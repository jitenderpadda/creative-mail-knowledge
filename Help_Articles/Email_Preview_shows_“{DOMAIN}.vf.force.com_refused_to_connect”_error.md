# Email Preview shows “{DOMAIN}.vf.force.com refused to connect” error

To resolve this issue, navigate to **Setup** ->**Session Settings**

1. Under **Trusted Domains for Inline Frames,** click **Add Domain**
2. Copy the current url from your browser address bar
3. Keep only the domain part which ends with [force.com](https://force.com)
4. Ensure to remove the **https://**
5. Paste this domain in the **Domain field** and the iFrame Type should be visualforce
6. **Save**

**![](https://s3.amazonaws.com/cdn.freshdesk.com/data/helpdesk/attachments/production/43483311306/original/uwCkW0aBw0Naw96gYZutlAwmXHxLTUpPXw.png?1714687548)**

The Email Preview page should now load correctly.
