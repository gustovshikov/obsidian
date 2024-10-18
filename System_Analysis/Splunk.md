

useful search commands
- Sort
- Stats
	- `stats count by <thing>`
- Table
- Uniq
- Dedup

The process of creating alerts can be split into four main steps:
1. **Search Query**
2. **Search Timing**
3. **Alert Triggers**
4. **Alert Actions**


https://docs.splunk.com/Documentation/UBA/5.4.1/GetDataIn/WindowsEventsUsedByUBA

| Event ID | Description                                                       |
| -------- | ----------------------------------------------------------------- |
| 4624     | An account was **SUCCESSFULLY logged on**                         |
| 4625     | An account **FAILED to log on**                                   |
| 4647     | User initiated **logoff**                                         |
| 4648     | A **logon** was attempted **USING EXPLICIT CREDENTIALS**          |
| 4649     | A **replay attack** was **DETECTED**                              |
| 4659     | A **handle to an object** was requested with **INTENT TO DELETE** |
| 4706     | A **new trust** was **CREATED** to a domain                       |
| 4720     | A **user account** was **CREATED**                                |
| 4726     | A **user account** was **DELETED**                                |
| 4732     | A **member was ADDED** to a security-enabled local group          |
| 4672     | Special Logon                                                     |
| 4740     | An account was locked out.                                        |
|          |                                                                   |

### Monitoring PowerShell Activity

- **Event ID 4688** helps detect when PowerShell is launched.
- **Event ID 4104** provides the actual script contents.
- **Event ID 4103** gives information about modules being loaded.