# Invoice Collector BETA 0.1.1 — reviewer quick test

No account, network service, credentials or real customer documents needed. Use a fresh Chrome profile. Install the review item and click its toolbar icon.

1. Download [demo.xml](invoice-review-demo.xml), a synthetic XML sample (not a real invoice).
2. Enter **Example GmbH** in Company or account label. Paste these two lines into Missing items:
   ```
   Hosting October
   Office supplies
   ```
3. Select **Create checklist**. Under Hosting October, select the downloaded XML. Leave Office supplies unresolved. Expected: 1 of 2 items associated.
4. Select **Download review batch**. Open the exported ZIP. Its manifest.json must list Hosting October as USER_ASSOCIATED and Office supplies as UNRESOLVED. The original XML bytes must be unchanged; its SHA-256 is recorded in the manifest. No actual identity verification, sending or filing occurs.
5. Reload the extension page. Expected: empty checklist and disabled export.

The local page processes only user-entered text and selected files. See [privacy policy](invoice-collector.md). Contact info@aimino.de for support. This is a manual local beta, not automatic invoice discovery.
