# Migrating from BeeFree to Creative Mail

The Creative Mail app is a more refined version of the BeeFree app and uses new Salesforce features such as Lightning Email Templates. Because of this during migration you will need to create new Email Templates from the existing ones but no need to worry, in order to make your lives simpler, we have created a nifty little script that will do most of the handling for you.

Just follow the simple steps mentioned below -

1. First, ensure that you have installed and set up [Creative Mail](https://creativemail.gitbook.io/knowledge/getting-started/creative_mail_user_guide)
2. Click on the gear icon on the top right and open the Developer Console
3. From the menu click on Debug and select Open Execute Anonymous Window
4. Copy and paste the snippet below to copy over your BeeFree Templates onto your new Creative Mail Templates

```
List<creativemail\_\_Creative\_Mail\_Template\_\_c> cmTemplateList = new List<creativemail\_\_Creative\_Mail\_Template\_\_c>();
List<BeeFree\_\_BeeFree\_Template\_\_c> bfTemplateList = [
 SELECT
 Id,
 Name,
 BeeFree\_\_Email\_Template\_Id\_\_c,
 BeeFree\_\_JSON\_Template\_\_c,
 BeeFree\_\_Recipient\_Type\_\_c,
 BeeFree\_\_Related\_To\_Type\_\_c
 FROM BeeFree\_\_BeeFree\_Template\_\_c
];

Set<Id> emailTempIds = new Set<Id>();
for (BeeFree\_\_BeeFree\_Template\_\_c bfTemplate : bfTemplateList) {
 emailTempIds.add(bfTemplate.BeeFree\_\_Email\_Template\_Id\_\_c);
}

Map<Id, EmailTemplate> emailTemplateMap = new Map<Id, EmailTemplate>(
 [SELECT Id, Subject FROM EmailTemplate WHERE Id IN :emailTempIds]
);

for (BeeFree\_\_BeeFree\_Template\_\_c bfTemplate : bfTemplateList) {
 creativemail\_\_Creative\_Mail\_Template\_\_c cmTemplate = new creativemail\_\_Creative\_Mail\_Template\_\_c();
 cmTemplate.Name = bfTemplate.Name.replace('\_', ' ') + ' clone';
 cmTemplate.creativemail\_\_JSON\_File\_1\_\_c = bfTemplate.BeeFree\_\_JSON\_Template\_\_c;
 cmTemplate.creativemail\_\_Recipient\_\_c = bfTemplate.BeeFree\_\_Recipient\_Type\_\_c;
 cmTemplate.creativemail\_\_Related\_To\_\_c = bfTemplate.BeeFree\_\_Related\_To\_Type\_\_c ==
 '--none--'
 ? null
 : bfTemplate.BeeFree\_\_Related\_To\_Type\_\_c;
 cmTemplate.creativemail\_\_Subject\_\_c = emailTemplateMap.get(
 bfTemplate.BeeFree\_\_Email\_Template\_Id\_\_c
 )
 ?.Subject;
 cmTemplateList.add(cmTemplate);
}

insert cmTemplateList;
```

5. Click on execute  
   ![](https://s3.amazonaws.com/cdn.freshdesk.com/data/helpdesk/attachments/production/43384553111/original/-ClXF7DeVMh_hBkpRhVOEyqo1jWfhXn-Hw.png?1673489449)
6. The last step you will need to perform is to go into each Creative Mail Template, click on the **Edit Template in Builder** button and then hit save in order to generate the new Lightning Email Template.

Please make sure to update the merge fields since the merge field syntax is different for Lightning Email Templates.

**NOTE:**

Please ensure to update the Creative Mail Template names as they need to be unique and will be appended with 'clone' during the migration process.

Feel free to reach out to us if you have any issues at [Contact Support](mailto:support@creativemail.io)
