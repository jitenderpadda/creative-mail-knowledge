# Email Preview shows “{DOMAIN}.vf.force.com refused to connect” error

To resolve this issue, navigate to **Setup** ->**Session Settings**

1. Under **Trusted Domains for Inline Frames,** click **Add Domain**
2. Copy the current url from your browser address bar
3. Keep only the domain part which ends with [force.com](https://force.com)
4. Ensure to remove the **https://**
5. Paste this domain in the **Domain field** and the iFrame Type should be visualforce
6. **Save**

![](../images/knowledge/email-preview-vf-error/uwCkW0aBw0Naw96gYZutlAwmXHxLTUpPXw.png)

The Email Preview page should now load correctly.
