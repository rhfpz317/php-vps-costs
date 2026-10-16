# php hosting: how a $10.99/year VPS compares to managed hosts, plus how to pick the right plan for WordPress or Laravel

PHP runs over 77% of all websites, so nearly every host on the market "supports PHP." The differences that actually matter sit around it: which PHP versions are available, how much control you get over php.ini, whether OPcache and Redis are in the picture, and what the whole thing costs by year two. Those differences split into two camps. Managed hosts run the stack for you and charge monthly — entry shared plans start at $1.99–$2.99/month, managed cloud around $11/month. A DIY VPS makes you the sysadmin and costs a fraction of that: RackNerd's KVM VPS plans start at **$9.89/year** for 768 MB and **$10.99/year** for 1 GB, and the promo rate is the rate you keep renewing at.

This guide covers both routes, then gets specific about RackNerd: the full special-plan lineup, which PHP version each OS template actually ships with, and how to match a plan to a WordPress site or a Laravel app with queue workers.

> **Quick picks**
>
> - Cheapest way to run a real PHP site, and you're comfortable in a terminal: RackNerd's **1 GB KVM** at **$10.99/year** handles a low-traffic WordPress install fine. 👉 See RackNerd's current VPS specials
> - Laravel with queues, Redis and MySQL on one box: the **2.5 GB** plan at $24.88/year is the sweet spot.
> - Never want to touch a server: go managed instead — shared plans from hosting.com, Hostinger or SiteGround start at $1.99–$2.99/month, and managed cloud at Cloudways starts at $11/month.

## What actually makes a host good for PHP?

Any host can execute a PHP file. The separation happens at version control and caching. A good PHP host keeps current versions (8.1, 8.2, 8.3) available, lets you switch versions per site, exposes php.ini values like memory_limit and max_execution_time, and pairs PHP with OPcache plus an object cache such as Redis. For anything more complex than a blog, the checklist grows: 256 MB+ memory limits, Composer for dependencies, and SSH access for command-line work.

Two traps are worth naming up front. Version rot is the first: PHP 7 reached end of life in November 2022, yet some free hosts still serve PHP 7 in 2026 — AwardSpace's free plan is the commonly cited example. No security patches, no compatibility with modern frameworks. The second trap is the sleeping free tier: free PaaS plans spin your service down between requests, which is fine for a demo and bad for an API that has to respond in milliseconds. An always-on $9.89/year VPS exists precisely for that gap.

## Managed PHP hosting vs a DIY VPS: where the money goes

Managed hosting sells convenience in monthly slices; a DIY VPS sells raw control and asks for your time instead. Neither is wrong — it depends on whether "patch the server tonight" sounds like a chore or a normal Tuesday.

| Host | Type | Entry price | PHP control |
| --- | --- | --- | --- |
| hosting.com | Shared | $1.99/mo | PHP 4.4–8.3, switchable in cPanel |
| Hostinger | Shared / VPS | $2.99/mo | PHP 5.2 through 8.x |
| SiteGround | Managed shared | $2.99/mo | PHP 7.4–8.3, per-site switching |
| Cloudways | Managed cloud | $11/mo | Current 8.x, switching handled for you |
| Kinsta | Managed WP | $30/mo | All PHP versions supported |
| DigitalOcean | DIY cloud VPS | $4/mo | PHP 7.x default, 8.x installable |
| RackNerd | DIY KVM VPS | $9.89/yr (~$0.82/mo) | Any version you install |

For context on where the managed tier stands: HostList's 2026 PHP hosting ranking puts SiteGround, Kinsta and Cloudways joint-first at 97/100 each. That's the convenience tier, and it's good — as long as your app fits its shape.

The catch sits at the bottom of the price range. Sub-$3 shared plans rarely allow long-running workers, custom daemons or Supervisor, so a Laravel app with Horizon queues gets CPU-throttled there. Renewals are the other gotcha: Hostinger's shared plans, for instance, run a classic intro-to-renewal cliff, where the cheap first term jumps at renewal.

A VPS flips both constraints. You set memory_limit yourself, you install Redis, you run cron and Supervisor, and nothing throttles your workers. You also inherit every sysadmin task that implies. That's the deal RackNerd offers, more cheaply than almost anyone — the company built its name on annual KVM deals posted to hosting forums like LowEndTalk rather than on marketing.

## RackNerd's KVM VPS plans and pricing

RackNerd sells unmanaged KVM VPS, and its annual specials start at $9.89/year. The popular tiers in the current special lineup:

| Plan | CPU / RAM | Storage | Bandwidth | Price (billed yearly) | Order |
| --- | --- | --- | --- | --- | --- |
| 768 MB KVM | 1 vCPU / 768 MB | 15 GB SSD | 750 GB | $9.89/yr | [ Order](https://bit.ly/my-rn) |
| 1 GB KVM | 1 vCPU / 1 GB | 20 GB SSD | 1 TB | $10.99/yr | [ Order](https://bit.ly/my-rn) |
| 2.5 GB KVM | 2 vCPU / 2.5 GB | 50 GB SSD | 3 TB | $24.88/yr | [ Order](https://bit.ly/my-rn) |
| 4 GB KVM | 3 vCPU / 4 GB | 65 GB SSD | 4 TB | $39.88/yr | [ Order](https://bit.ly/my-rn) |
| 8 GB KVM | 4 vCPU / 8 GB | 100 GB SSD | 6 TB | $78.88/yr | [ Order](https://bit.ly/my-rn) |

A few things the table doesn't show:

- KVM virtualization with full root access, a 1 Gbps network port, SSD storage, and a dedicated IPv4 address included on every plan.
- Data center locations in Los Angeles, San Jose, Seattle, Dallas, Chicago, New York and Amsterdam, chosen at order time.
- RackNerd rotates its specials a few times a year, and intermediate sizes (1.5 GB, 2 GB, 3 GB, 5 GB, 6 GB) appear in the lineup between the tiers above. Exact storage and bandwidth numbers can shift between promo cycles, so treat the cart total as the source of truth.
- Monthly billing exists, but the annual specials are where the value lives — the same specs cost several times more month to month.

## Which PHP version will you actually get on a RackNerd VPS?

Whatever your OS template ships with — and on current templates that's reasonably modern, with a one-command path to the newest release.

| OS template | PHP out of the box | Newer versions via |
| --- | --- | --- |
| Ubuntu 24.04 LTS | PHP 8.3 | ondrej/php PPA |
| Ubuntu 22.04 LTS | PHP 8.1 | ondrej/php PPA |
| Debian 12 | PHP 8.2 | sury.org repository |
| AlmaLinux 9 / Rocky 9 | PHP 8.0 module | Remi repository |

On a shared host, the provider decides which versions appear in the panel and when. On a RackNerd box, you run that schedule yourself: add the right repository and you can install PHP 8.3 or 8.4 the day you need it. You also get everything ranking articles keep telling you to check for — full control over memory_limit, max_execution_time and upload sizes in php.ini, OPcache you enable and tune, Redis or Memcached one package install away, plus cron and Supervisor for scheduled jobs and queue workers. That last group of features is exactly what sub-$3 shared hosting won't let you run. 👉 Check RackNerd's current plans and pricing

## What a year — and three years — actually costs

The sticker price on RackNerd's special plans is the price you keep paying: the promo rate renews at the same amount for as long as you keep the plan active.

Run the math. The 1 GB plan works out to about $0.92/month, or roughly $33 over three years. The 2.5 GB plan is about $2.07/month, $74.64 over three. Compare that with the managed column: SiteGround's $2.99/month intro pricing already totals $107.64 over three years before any renewal adjustment, Cloudways runs $132 per year, and Kinsta runs $360 per year. RackNerd's 2.5 GB plan costs less annually than a single month of Kinsta — and hands you the admin work in exchange. 👉 Check RackNerd's current annual specials

That renewal behavior is the quiet differentiator here. Plenty of budget shared hosts advertise a low first term and step the price up at renewal; RackNerd's specials lock instead, which makes multi-year cost planning unusually boring — in a good way.

## Which plan fits which PHP stack?

Match the plan to what the server has to hold, not to what's cheapest:

- **768 MB ($9.89/yr)** — lean PHP scripts, a small blog, learning. MySQL on the same box is workable but tight; add swap.
- **1 GB ($10.99/yr)** — one low-traffic WordPress site, small Laravel APIs without background workers, staging environments.
- **2.5 GB ($24.88/yr)** — Laravel plus MySQL, Redis and Horizon workers; WooCommerce with modest traffic.
- **4 GB ($39.88/yr)** — several mid-traffic sites on one server, heavier WooCommerce, or production plus a staging copy.
- **8 GB ($78.88/yr)** — consolidated servers and busy databases once the side projects grow up.

One honest caution: the 768 MB plan is priced like a learning tool and behaves like one. If a real site is going on it, spend the extra $1.10 a year and take the 1 GB plan. 👉 Compare RackNerd's KVM plans side by side

## What RackNerd doesn't give you

Scope check, so nobody orders the wrong product: this is self-managed hosting. Nobody at RackNerd tunes your php.ini, applies stack updates, or debugs a broken PHP-FPM pool — that's your job. Their 24/7 ticket support covers the hardware, network and platform side, which is the standard arrangement for unmanaged budget providers.

Also absent, by design: a licensing-included control panel (cPanel isn't bundled; free panels like Hestia or CloudPanel are the usual workaround), managed backups (roll your own with snapshots or off-site scripts), one-click app installers, and even SSL is self-serve — Let's Encrypt via certbot, which is free and automatic once configured. If any line in that list sounds like a dealbreaker, the managed tier exists for exactly this reason: shared plans at $1.99–$2.99/month or Cloudways from $11/month buy back those chores, and cost several times more per year doing it.

## FAQ

**Can I host WordPress on a RackNerd VPS?**
Yes. There's no one-click installer, so you'll set up a LEMP stack and WordPress yourself — an hour or so the first time if you follow a solid guide. Full root access means no artificial limits afterwards.

**Do the promo prices renew at the same rate?**
Yes. The policy on RackNerd's special pricing is that the rate you sign up at is the rate you renew at, for as long as the plan stays active.

**Is a RackNerd VPS enough for Laravel?**
For development and small production apps, yes — pick 2.5 GB or more. Laravel with Horizon workers, Redis and MySQL on one box wants that headroom.

**Can I run an old PHP version like 5.6?**
Technically you can install anything you're willing to maintain. Practically, don't: PHP 5.6 and 7.x are end-of-life, and controlling your own server is largely about being able to run a current, patched version.

## Before you order

The short version of the decision: cheapest workable option for one real site → the 1 GB plan at $10.99/year. Laravel, queue workers or multiple services → 2.5 GB at $24.88/year. Multiple growing sites → 4 GB. Allergic to terminals → the managed route described above, with no hard feelings.

Two last checks before checkout. Pick the data center nearest your visitors — Amsterdam for European traffic, the US West Coast for Pacific-facing audiences. And remember these are annual plans, so the commitment is per year, not per month; at $10.99, that math usually works out in your favor. 👉 Pick your RackNerd plan here
