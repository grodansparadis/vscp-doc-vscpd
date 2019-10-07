# Remote variables for decision matrix manipulation

This is remote variables that can be used to read and manipulated the decision matrix. Only remote variables related to the full decision matrix will show up in list. The row specific remote variables (vscp.dm.n......) will not.

The *rwx* column below stands for **r**ead **w**rite e**x**ecute and is rights needed to read/write/execute variables for the admin user, group users, all users
. So rw-rw-rw- means all users have read/write access. r-------- that only the admin user can read the remote variable.

Writing some variables execute commands such as adding or deleting something. Execute permission is for this type of variables.

| Stock variable                           | type     | rwx        | Description                                                                                                                                                                                                                                                             |
| ---------------------------------------- | -------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **vscp.dm**                              | string   | r--r--r--  | Read full decsion matrix. Each row is returned on the comma separated form with a carrige return between rows.                                                                                                                                                          |
| **vscp.dm.enable**                       | bool     | rw-r--r--  | Read write enable flag for decision matrix.                                                                                                                                                                                                                             |
| **vscp.dm.count**                        | long     | r--r--r--  | Read total number of decision matrix rows including disabled rows                                                                                                                                                                                                       |
| **vscp.dm.count.active**                 | long     | r--r--r--  | Read number of active (enabled) decision matrix rows including disabled rows                                                                                                                                                                                            |
| **vscp.dm.path-db**                      | string   | r--r--r--  | Get full path to remote variable database. See configure to set it.                                                                                                                                                                                                     |
| **vscp.dm.path-xml**                     | string   | r--r--r--  | Get full path to remote variable XML file. See configure to set it.                                                                                                                                                                                                     |
| **vscp.dm.add**                          | string   | --x----    | Add a decision matrix row. The row should be given on the standard comma separated form.                                                                                                                                                                                |
| **vscp.dm.delete**                       | long     | --x----    | Delete a decision matrix row.                                                                                                                                                                                                                                           |
| **vscp.dm.n**                            | string   | rw-r--r--  | Read or write a decision matrix row n (vscp.dm.1 is row one and so on). The format for the row is the standard comma separated format.                                                                                                                                  |
| **vscp.dm.n.id**                         | long     | r--r--r--  | Read the id field for a decision matrix row.                                                                                                                                                                                                                            |
| **vscp.dm.n.enable**                     | bool     | rw--r--r-- | Read/write the enable field for a decision matrix row.                                                                                                                                                                                                                  |
| **vscp.dm.n.groupid**                    | string   | rw--r--r-- | Read/write the groupid field for a decision matrix row.                                                                                                                                                                                                                 |
| **vscp.dm.n.mask**                       | string   | rw--r--r-- | Read/write the mask field for a decision matrix row. Mask should is on standard comma separated format.                                                                                                                                                                 |
| **vscp.dm.n.mask.priority**              | integer  | rw--r--r-- | Read/write the mask priority field part for a decision matrix row.                                                                                                                                                                                                      |
| **vscp.dm.n.mask.class**                 | integer  | rw--r--r-- | Read/write the mask VSCP class field part for a decision matrix row.                                                                                                                                                                                                    |
| **vscp.dm.n.mask.type**                  | integer  | rw--r--r-- | Read/write the mask VSCP type field part for a decision matrix row.                                                                                                                                                                                                     |
| **vscp.dm.n.mask.guid**                  | guid     | rw--r--r-- | Read/write the mask GUID field part for a decision matrix row.                                                                                                                                                                                                          |
| **vscp.dm.n.filter**                     | string   | rw--r--r-- | Read/write the filter field for a decision matrix row. Filter should is on standard comma separated format.                                                                                                                                                             |
| **vscp.dm.n.filter.priority**            | integer  | rw--r--r-- | Read/write the filter priority field part for a decision matrix row.                                                                                                                                                                                                    |
| **vscp.dm.n.filter.class**               | integer  | rw--r--r-- | Read/write the filter VSCP class field part for a decision matrix row.                                                                                                                                                                                                  |
| **vscp.dm.n.filter.type**                | integer  | rw--r--r-- | Read/write the mask VSCP type filter part for a decision matrix row.                                                                                                                                                                                                    |
| **vscp.dm.n.filter.guid**                | guid     | rw--r--r-- | Read/write the filter GUID field part for a decision matrix row.                                                                                                                                                                                                        |
| **vscp.dm.n.allowed**                    | string   | rw--r--r-- | Read/write the allowed fields part for a decision matrix row. Format is comma separated "start,end,weekdays,time".                                                                                                                                                      |
| **vscp.dm.n.allowed.start**              | datetime | rw--r--r-- | Read/write the allowed start date/time field for an action on a decision matrix row. "*" is "always". Date time is set on ISO form as YYYY-MM-DDTHH:MM:SS                                                                                                               |
| **vscp.dm.n.allowed.end**                | datetime | rw--r--r-- | Read/write the allowed start date/time field for an action on a decision matrix row. "*" is "always". Date time is set on ISO form as YYYY-MM-DDTHH:MM:SS                                                                                                               |
| **vscp.dm.n.allowed.weekdays**           | string   | rw--r--r-- | Read/write the allowed weekdays for an action on a decision matrix row. "*" is "always". The format is "mtwtfss" fir allowed days and using "-" for a day that is NOT allowed. So for example "mt-tfss" allow the action to be performed all days except on wednesdays. |
| **vscp.dm.n.allowed.monday**             | boolean  | rw--r--r-- | Read/write the allowed weekday monday for an action on a decision matrix row. True means allowed day. False means diallowed day.                                                                                                                                        |
| **vscp.dm.n.allowed.tuesday**            | boolean  | rw--r--r-- | Read/write the allowed weekday tuesday for an action on a decision matrix row. True means allowed day. False means diallowed day.                                                                                                                                       |
| **vscp.dm.n.allowed.wednesday**          | boolean  | rw--r--r-- | Read/write the allowed weekday wednesday for an action on a decision matrix row. True means allowed day. False means diallowed day.                                                                                                                                     |
| **vscp.dm.n.allowed.thursday**           | boolean  | rw--r--r-- | Read/write the allowed weekday thursday for an action on a decision matrix row. True means allowed day. False means diallowed day.                                                                                                                                      |
| **vscp.dm.n.allowed.friday**             | boolean  | rw--r--r-- | Read/write the allowed weekday friday for an action on a decision matrix row. True means allowed day. False means diallowed day.                                                                                                                                        |
| **vscp.dm.n.allowed.saturday**           | boolean  | rw--r--r-- | Read/write the allowed weekday saturday for an action on a decision matrix row. True means allowed day. False means diallowed day.                                                                                                                                      |
| **vscp.dm.n.allowed.sunday**             | boolean  | rw--r--r-- | Read/write the allowed weekday sunday for an action on a decision matrix row. True means allowed day. False means diallowed day.                                                                                                                                        |
| **vscp.dm.n.allowed.time**               | string   | rw--r--r-- | Read/write the allowed time field for an action on a decision matrix row. See the description of the decision matrix for format. Setting to '*' means always.                                                                                                           |
| **vscp.dm.n.checkindex**                 | boolean  | rw--r--r-- | Read/write the checkindex field flag for an action on a decision matrix row.                                                                                                                                                                                            |
| **vscp.dm.n.index**                      | integer  | rw--r--r-- | Read/write the index field for an action on a decision matrix row.                                                                                                                                                                                                      |
| **vscp.dm.n.checkzone**                  | boolean  | rw--r--r-- | Read/write the checkzone field flag for an action on a decision matrix row.                                                                                                                                                                                             |
| **vscp.dm.n.zone**                       | integer  | rw--r--r-- | Read/write the zone field for an action on a decision matrix row.                                                                                                                                                                                                       |
| **vscp.dm.n.checksubzone**               | boolean  | rw--r--r-- | Read/write the checksubzone field flag for an action on a decision matrix row.                                                                                                                                                                                          |
| **vscp.dm.n.subzone**                    | integer  | rw--r--r-- | Read/write the subzone field for an action on a decision matrix row.                                                                                                                                                                                                    |
| **vscp.dm.n.measurement**                | string   | rw--r--r-- | Read/write the measurement values for an action on a decision matrix row. Format is a comma separated list on the form "enable,value,unit,compare-code/compare-string".                                                                                                 |
| **vscp.dm.n.measurement.enable**         | boolean  | rw--r--r-- | Read/write the checkmeasurement field flag for an action on a decision matrix row.                                                                                                                                                                                      |
| **vscp.dm.n.measurement.value**          | double   | rw--r--r-- | Read/write the measurement value for an action on a decision matrix row.                                                                                                                                                                                                |
| **vscp.dm.n.measurement.unit**           | integer  | rw--r--r-- | Read/write the measurement unit for an action on a decision matrix row.                                                                                                                                                                                                 |
| **vscp.dm.n.measurement.compare-string** | string   | rw--r--r-- | Read/write the measurement compare-string for an action on a decision matrix row.                                                                                                                                                                                       |
| **vscp.dm.n.measurement.compare-code**   | integer  | rw--r--r-- | Read/write the measurement compare-code for an action on a decision matrix row.                                                                                                                                                                                         |
| **vscp.dm.n.comment**                    | string   | rw--r--r-- | Read/write the free text comment for a decision matrix row.                                                                                                                                                                                                             |
| **vscp.dm.n.count-trigger**              | long     | rw--r--r-- | Read/write the trigger count (number of times the action has been executed) for a decision matrix row. Writing any value resets the counter.                                                                                                                            |
| **vscp.dm.n.count-error**                | long     | rw--r--r-- | Read/write the error count for a decision matrix row. Writing any value resets the counter.                                                                                                                                                                             |
| **vscp.dm.n.error**                      | string   | r--r--r--  | Read the last error string for a decision matrix row.                                                                                                                                                                                                                   |
| **vscp.dm.n.error-string**               | string   | r--r--r--  | Read the last error string for a decision matrix row.                                                                                                                                                                                                                   |

{% include "./bottom_copyright.md" %}