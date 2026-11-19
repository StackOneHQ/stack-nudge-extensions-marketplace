# Security

A merged extension runs on people's Macs as them, with nothing sandboxing it, so a hole in one
matters. If you find one, report it privately rather than in an issue, a pull request or a
public channel.

## Reporting

- Email support@stackone.com, saying in the subject that it's a security report for
  stack-nudge-extensions-marketplace. A problem in the app itself goes to StackOneHQ/stack-nudge's
  SECURITY.md.
- Say what you found, how to reproduce it and what it lets someone do: which extension, and which
  commit or release.
- Leave out real tokens and anyone's data. A stand-in shows the problem just as well.

Please give the team the chance to fix it before telling anyone else.

## What counts

Anything that lets an extension or a package do more than it should: an extension that runs or
writes outside its own directory, sends something PRIVACY.md doesn't list, or keeps a secret
anywhere it shouldn't; a package that gets past `package-extensions.sh validate` with a symlink,
an escaping path or a tier it wasn't given; a workflow that runs untrusted input or leaves a write
token behind.

## Supported versions

Only the latest release and `main`. Nothing older gets a fix.
