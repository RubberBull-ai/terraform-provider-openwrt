# Router firewall as code

Manage the home GL.iNet router's (OpenWrt, 192.168.0.1) firewall with Terraform,
through this fork of joneshf/terraform-provider-openwrt, so the IoT VLAN
(192.168.10.0/24, no internet) can reach a local Roborock server.

## Owner's requirements

All quotes from the owner, 2026-10-17.

- "Can we tf that shit with luci" - manage the router's LuCI/UCI config with Terraform.
- "How hard would it be for you to code a openwrt extension for joneshf/openwrt" -
  extend joneshf/terraform-provider-openwrt rather than use another provider.
- "Oky so lets goo it will live under rubberbull" - the fork is
  RubberBull-ai/terraform-provider-openwrt. Said in reply to the proposed plan: a first
  PR adding `openwrt_firewall_rule` with acceptance tests, a second adding
  `openwrt_system_timeserver`.
- "Thats fine I as long a shit is not periodic" - GL.iNet's own management layer may
  rewrite the firewall config when its admin panel is used; that is acceptable, a
  periodic rewrite is not.

## Milestones

| # | Milestone | Delivered by |
|---|---|---|
| M1 | `openwrt_firewall_rule` resource and data source (UCI `firewall.rule`), with acceptance tests | PR 1 |
| M2 | `openwrt_system_timeserver` resource and data source (UCI `system.timeserver`), with acceptance tests | PR 2 |
| M3 | Confirmed on the live router that GL.iNet does not rewrite the firewall config periodically | check on the router, recorded in PR 1 or 2 |

Nothing else.

## Open questions for the owner (not requirements)

- Publishing the fork to the Terraform/OpenTofu registry (needs a GPG signing key and a
  release workflow), so Atlantis and the talos cdktf provider generator can use it.
- A talos cdktf stack for the router, applied by Atlantis.
- Installing `luci-mod-rpc` on the router (the RPC endpoint returns 404 today).
- Enabling GitHub Actions on the fork so the existing test workflow runs.
