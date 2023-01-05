> An email flavor of [mastodon digest](https://github.com/mauforonda/mastodon_digest), originally forked from [hodgesmr/mastodon_digest](https://github.com/hodgesmr/mastodon_digest)

**Mastodon Email Digest** scans posts you haven't yet seen in your timeline and sends the most popular ones to your inbox 🦣 → ✉️

![](howitlooks.png "How it would look in your inbox")

## To run your own

1. Fork this repository
2. Create repository secrets (`Settings` → `Secrets/Actions` → `New repository secrets`) for:
  - `MASTODON_BASE_URL`: the url of your instance, like `https://mastodon.social`
  - `MASTODON_USERNAME`: your user name, like `Gargron`
  - `MASTODON_TOKEN`: a token you request in your instance settings under `Preferences` → `Development`
  - `MAIL_SERVER`: `smtp.gmail.com` the server you want to send emails from, `smtp.gmail.com` if you use gmail.
  - `MAIL_SERVER_PORT`:  the server port you want to send emails from, `465` if you use gmail.
  - `MAIL_USERNAME`: your username in the server.
  - `MAIL_PASSWORD`: your email password. If you're using gmail, use an [app password](https://support.google.com/accounts/answer/185833?hl=en) for `Mail` and any device, after setting up 2-step verification.
  - `MAIL_DESTINATION`: the address you want to get the digest on, like `gargrons_inbox@gmail.com`
3. Adjust the [github workflow](.github/workflows/update.yml) however you want
  - edit `cron` to define how often you want the digest to run
  - edit the command `python run.py -n 24 -s SimpleWeighted -t lax` with your own preferences for:
```
  -n {1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24}
                        The number of hours to consider (default: 12)
  -s {ExtendedSimple,ExtendedSimpleWeighted,Simple,SimpleWeighted}
                        Which post scoring criteria to use. Simple scorers take a geometric
                        mean of boosts and favs. Extended scorers include reply counts in
                        the geometric mean. Weighted scorers multiply the score by an
                        inverse sqaure root of the author's followers, to reduce the
                        influence of large accounts. (default: SimpleWeighted)
  -t {lax,normal,strict}
                        Which post threshold criteria to use. lax = 90th percentile, normal
                        = 95th percentile, strict = 98th percentile (default: normal)
```
4. Enable github actions under `Settings` → `Actions/General`. 


If you've set your secrets right you'll receive an email at the time you specified. And if you want to test it right away you can always go to the `Actions` tab, select the `My Mastodon Email Digest` workflow and `Run workflow`, which should send you and email in about a minute ✉️