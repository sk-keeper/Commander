Commander Plugin for Generating/Rotating SSH keys
----

This plugin generates/rotates SSH keys for the provided user on the local system.  The 'Login' field of the Keeper record defines the user account which is being rotated. The 'password' field is used as the optional passphrase to encrypt the private key.  The resulting SSH key information is stored in custom fields and sync'd to your Keeper vault.  Any Keeper user or Keeper Shared Folder associated with the record is updated instantly.

### Dependencies 

1) Add the following Custom Fields to the Keeper record

```
Name: cmdr:plugin
Value: sshkey
```

2) The plugin will use the 'Login' field as the username of the 'passwd' command

### Optional custom fields

To specify the rules for password complexity to use add a custom field

```
Name: cmdr:rules
Value: 4,6,3,8
```

This would generate a new password with :
```
  4 uppercase characters
  6 lowercase characters
  3 numerical characters
  8 punctuation characters
```

### Auto-command execution

You can automate SSH key rotations using this plugin

Example:

```
{                                                                               
    "debug":false,
    "server":"https://keeperapp.com/v2/",
    "user":"admin@company.com",
    "password":"somereallystrongpassword",
    "mfa_token":"vFcl44TdjQcgTVfCMlUw0O9DIw8mOg8fJypGOlS_Rw0WfXbCD9iw",
    "mfa_type":"device_token",
    "commands":["d", "r 3PMqasi9hohmyLWJkgxCWg"]
}
```

In this example above, we are telling Commander to first download and decrypt records, then generate SSH keys for the record ID 3PMqasi9hohmyLWJkgxCWg. The custom fields in the record give the plugin the information it needs to rotate the SSH key. Each unique record in the Keeper system is represented by a unique record UID.  Use the "l" or "s" command in Commander's interactive mode ('keeper shell') to display the record UIDs in your account.

