# Privacy

What each extension reads on the Mac, what it sends, and where it's kept. Update this in the same
pull request as any change to it. An installed extension is a separate program that stack-nudge
runs, and whatever network calls it makes are its own. What stack-nudge itself sends, including
fetching this catalogue, is in StackOneHQ/stack-nudge's PRIVACY.md.

## away

Listens for the Bluetooth LE signal your phone already sends, to tell when you've left the Mac.
It reads the names of the devices paired with the Mac, and the names and signal strength of the
ones it hears nearby, for the phone picker and its status line. Nothing is installed on the phone
and nothing leaves the Mac. It keeps no data on disk, only the program it compiles itself into,
in `.build/` in its own directory. Whether to lock the screen is stack-nudge's own setting, not
the extension's.

## derby

The Token Derby, a shared horse race scored on tokens produced. Off until you set an
organisation. When set, it makes two GET requests (that organisation's race list, then the race
it picks) to `token-derby.mauricode.co.uk` by default, a third-party service not operated by
StackOne and covered by its own privacy policy. The endpoint can be changed in its settings and
must be `https`. It is read-only: what leaves your machine is the organisation name you typed,
your IP address and a `stack-nudge` user agent. Nothing about your sessions or usage is sent.

## pylon

Customer issues in your Pylon workspace that are waiting on a response. Off until you set a Pylon
API token. When set, it asks `api.usepylon.com` (or `api.eu.usepylon.com`) for changes every 3
minutes by default (1 to 60, in its settings), including while the tab is hidden, so it can post
a banner before a first-response SLA runs out. It sends the token, your IP address and a
`stack-nudge` user agent, and reads issues, their messages, accounts and users. The one thing it
writes is when you mark an issue as spam (x twice on its row): that issue is tagged Spam and
closed.

Issue titles, account names and the first line of each issue's latest message are shown in the
tab; banners show issue titles and account names, and so appear in Notification Center and,
depending on your macOS settings, on the lock screen. A cache is kept in its own directory: the
issues waiting on a response (title, number, link, state, source, assignee, account and SLA
times), account names and owners, the workspace's users (names and emails), and those message
previews, readable only by you. Nothing about your sessions or usage is sent.

## system

CPU, memory and disk usage, from `ps`, `vm_stat`, `sysctl` and `df`. Makes no network calls and
keeps nothing.
