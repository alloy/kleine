# Kleine

A minimal public homepage and **draft** privacy policy for a privately operated,
OpenClaw-powered personal AI assistant. Plain HTML, shared CSS, a local SVG
favicon, and a small inline theme-detection script. No build, packages, backend,
authentication, database, analytics, cookies, or remote runtime assets.

**The files are ready for static hosting, not for submission as a final privacy
policy.** Complete the owner-review checklist below before production publication
or Google review. Deploying a website does not establish policy compliance,
Google verification, or approval.

## Files and local preview

```text
index.html
privacy/index.html
assets/styles.css
assets/favicon.svg
.nojekyll
README.md
```

From the repository root, run:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Open `http://127.0.0.1:8000/` and `http://127.0.0.1:8000/privacy/`.
Stop the preview with Ctrl+C. It is only a local preview, not production hosting.
Links and assets are relative, so both a GitHub Pages project subpath and a custom
domain work without changing HTML paths.

The site follows the browser's light/dark preference on page load. All content
also works without JavaScript, including automatic light/dark CSS fallback.
For visual checks, append `?scoutTheme=light` or `?scoutTheme=dark` to either URL.
There is no stored theme preference.

## Owner review: required before publication

- Confirm all enabled gog permissions and data categories match the policy;
  request only the scopes actually needed.
- Verify actual credential and operational-data storage, access controls,
  safeguards, logs, backups, retention, and deletion. The draft makes no
  unverified encryption or security-certification claims.
- Identify configured AI and other service providers. Disclose their relevant
  processing, retention, human-access, and deletion practices. Verify applicable
  Google policy restrictions, including provider use of Google data for training
  or improving generalized AI models, and obtain required user consent.
- Establish and describe an actual privacy/deletion request process.
- Replace the **not yet configured** contact placeholder with a monitored,
  dedicated support address or public contact method accepted by Google.
  Configure the required support email in Google Auth Platform as well.
  Do not publish a personal address.
- Verify actual behavior against the Google API Services User Data Policy,
  Limited Use requirements, and applicable Gmail/Workspace policies. Replace
  draft language with accurate, owner-approved disclosures; remove the review
  notice and verification notes only after resolving them. Update the policy's
  date and draft references in its description and Open Graph metadata.
- Review every public file for personal information, credentials, internal
  endpoints, and infrastructure details. GitHub serves repository files publicly;
  never add credentials, tokens, private assistant configuration, or real user data.
  If the repository itself is public, its history and commit metadata are also public.

## 1. Enable GitHub Pages

1. Push this repository to GitHub. Use a public repository unless your plan supports
   Pages from a private repository; the website itself must be publicly accessible.
2. In **Settings → Pages → Build and deployment**, choose **Deploy from a branch**.
   Select your published branch (for example `main`) and **/ (root)**, then save.
3. Wait for the Pages deployment to finish. Open the published URL shown in
   Settings and check both pages in a signed-out browser.

`.nojekyll` allows direct static publishing. No custom GitHub Actions workflow is
necessary. Pages may use a managed deployment workflow internally.

## 2. Configure a custom domain and DNS

No real domain or `CNAME` file is included. `example.com`, `kleine.example.com`,
`OWNER`, and `REPOSITORY` below are placeholders; replace them with your values.

1. Register a domain you control. First verify it for GitHub Pages in your
   account/organization **Settings → Pages**, using GitHub's supplied DNS TXT
   record. This verification is separate from Google Search Console.
2. In the repository's **Settings → Pages → Custom domain**, enter your chosen
   hostname, for example `kleine.example.com`, and save **before pointing DNS at
   GitHub**. Branch-based publishing creates a `CNAME` file with that hostname.
   Pull that commit locally and preserve it in future pushes. Do not add a scheme,
   path, or placeholder domain to `CNAME`.
3. For a subdomain, add this DNS record at your DNS provider:

   | Type | Name | Value |
   | --- | --- | --- |
   | CNAME | `kleine` | `OWNER.github.io` |

   Use the GitHub user/organization that owns the site. The target has no
   `https://`, repository name, or path. Remove conflicting records at that same
   hostname; do not remove unrelated domain records.

4. If you choose the apex domain (`example.com`) instead, configure ALIAS/ANAME
   to `OWNER.github.io` if supported, or all four GitHub Pages A records:

   ```text
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```

   Optional IPv6 uses the current AAAA values in GitHub's documentation. Do not
   use wildcard DNS. DNS changes may take up to 24 hours.

See GitHub's current [custom domain instructions](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
and [domain verification instructions](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)
before making changes.

## 3. Enable HTTPS

After GitHub's DNS check succeeds and its certificate is provisioned, select
**Enforce HTTPS** in **Settings → Pages**. This option may take up to 24 hours to
become available. Resolve DNS or certificate errors using
[GitHub's HTTPS guidance](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https).
Verify both final HTTPS URLs load without certificate warnings or mixed content
and that HTTP redirects to HTTPS.

## 4. Verify ownership in Google Search Console

1. Open [Google Search Console](https://search.google.com/search-console/about)
   using a Google Account associated with the OAuth project's Owner or Editor role.
2. Add a **Domain** property for the registrable domain, such as `example.com`
   (not a scheme or path).
3. Add the exact DNS TXT record Google supplies at your DNS provider and verify.
   Keep that record in place. Domain-property verification covers its subdomains.
4. Ensure that the verifying account is a verified owner in Search Console and
   remains associated with the Google Cloud project.

Use the registrable domain: for `kleine.example.co.uk`, that is `example.co.uk`,
not `co.uk`. Do not use a shared `github.io` domain as your custom authorized
domain. A domain you control makes the ownership relationship explicit.

## 5. Configure Google OAuth Branding

In the correct Google Cloud project, open **Google Auth Platform → Branding**.
Use app name **Kleine**, a monitored dedicated user-support email, and appropriate
developer contact information. Do not publish personal contact details on the site.
With your actual domain substituted:

| Field | Example value |
| --- | --- |
| Application homepage | `https://kleine.example.com/` |
| Privacy policy | `https://kleine.example.com/privacy/` |
| Authorized domain | `example.com` |

The homepage and policy must be public, on the same domain, and consistent with
the app's functionality and requested scopes. The homepage links prominently to
the policy. Absolute `og:url` and canonical metadata are intentionally omitted
until a real hostname is known; no URL substitution is needed for the site to work.

**Keep gog's Desktop app OAuth client.** This website does not implement OAuth.
Do not create a web client, callback page, JavaScript origin, or redirect endpoint
for it. Never add OAuth client credentials or access/refresh tokens to this repository.
Authorization and authorized-user restrictions remain in the assistant's environment,
not on this informational site.

### Publishing is not verification

For an External OAuth app, publishing status is managed under **Audience**.
When appropriate, use **Publish app** to transition from **Testing** to
**In production**. This is separate from branding verification/publication and
sensitive/restricted scope verification. Follow the actual console requirements:
Google may require **Verify Branding**, then **Publish branding**, and further
review under the Verification Center.

Google documents that refresh tokens issued to External apps in **Testing**
expire after seven days unless only basic identity scopes are requested. Gmail
and calendar access do not fall under that basic-identity exception. Moving to
production removes that testing-specific condition for new authorizations; it
does not make tokens permanent. After publishing, reauthorize gog as needed to
replace testing-era grants/tokens, without placing any of them in this website.

Production status does not by itself verify the app, remove unverified-app
warnings or user limits, or grant access to restricted scopes. Gmail permissions
can require sensitive/restricted scope verification and, where applicable, a
security assessment. Google documents some personal-use verification exceptions;
confirm eligibility rather than assuming it. A private family audience does not
make an External app an Internal Workspace app. This website neither enforces nor
expands access to the assistant.

Official references:

- [Branding, domain, and homepage requirements](https://developers.google.com/identity/protocols/oauth2/production-readiness/brand-verification)
- [Refresh-token expiration](https://developers.google.com/identity/protocols/oauth2#expiration)
- [Google API Services User Data Policy and Limited Use](https://developers.google.com/terms/api-services-user-data-policy)
- [Workspace API user-data policy, including AI restrictions](https://developers.google.com/workspace/workspace-api-user-data-developer-policy)
- [Restricted-scope verification](https://developers.google.com/identity/protocols/oauth2/production-readiness/restricted-scope-verification)

## Deployment checklist

- [ ] Resolve every privacy draft note, configure dedicated support, and approve the final policy.
- [ ] Push to GitHub and enable branch/root Pages publishing.
- [ ] Verify the custom domain with GitHub; set the Pages hostname, then DNS.
- [ ] Enable HTTPS; test homepage, policy, navigation, and favicon on the final domain.
- [ ] Verify the registrable domain in Google Search Console.
- [ ] Enter final URLs, authorized domain, support contact, and actual scopes in Google Auth Platform.
- [ ] Handle publishing and any required verification separately; reauthorize gog if needed.
