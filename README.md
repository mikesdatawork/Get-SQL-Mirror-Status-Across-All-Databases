![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

#  Get SQL Mirror Status Across All Databases
**Post Date: August 27, 2015**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process    <div>
Use this logic to get the Mirrored Status across all databases.
---
## SQL-Logic
```SQL

use master;
set nocount on
declare @get_database_mirroring_state varchar(max)
set @get_database_mirroring_state = ''
select @get_database_mirroring_state = @get_database_mirroring_state + 'declare @monitorresults_' + cast(database_id as varchar(2)) + ' as table (
database_name varchar(255)
, role int
, mirror_state tinyint
, witness_status tinyint
, log_generat_rate int
, unsent_log int
, sent_rate int
, unrestored_log int
, recovery_rate int
, transaction_delay int
, transaction_per_sec int
, average_delay int
, time_recorded datetime
, time_behind datetime
, local_time datetime
);
insert into @monitorresults_' + cast(database_id as varchar(2)) + ' exec msdb..sp_dbmmonitorresults
@database_name = ''' + upper(DB_NAME(database_id)) + '''
, @mode = 0
, @update_table = 0;
select
''server'' = upper(@@servername)
, database_name
, ''role'' =
case role
when ''1'' then ''Principal''
when ''2'' then ''Mirror''
end
, average_delay
, ''mirror_state'' =
case mirror_state
when ''0'' then ''Suspended''
when ''1'' then ''Disconnected''
when ''2'' then ''Synchronizing''
when ''3'' then ''Pending Failover''
when ''4'' then ''Synchronized''
end
```

[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)





---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

