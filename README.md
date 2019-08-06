Access Control
=======

Access Control Config Checker provides the ability to check if all interfaces provided by domain service is configured as required by Access Control middleware.

The checker will scan proto folder for service interfaces, compare them with those in config file and then list missing interfaces if any.

### Access Control Config Checker Usage
Usage
-----

First step: Set environment variables for accessing the MYSQL database. the default value of these environment variables is as shown below. you can set it up or not, depending on your needs.

          $ export ACL_MYSQL_USERNAME=root
          $ export ACL_MYSQL_PASSWORD=root
          $ export ACL_MYSQL_DATABASE=fwmrm_oltp
          $ export ACL_MYSQL_SERVER=localhost
          $ export ACL_MYSQL_PORT=3306
          
Second step:

```make && bin/access_control checker -d partner_service```
```console
foo@bar:access_control$ make
go build -o bin/access_control
foo@bar:access_control$ bin/access_control checker -d partner_service
Checking missing interfaces in config path  
error in /proto.BuyerService/GetBuyers: markets.read_oly is not found in database
error in /proto.BuyerService/GetBuyers: MARKETS_MANAGEMNT is not found in database
method /proto.DealService/GetDSPDeals is missing in the ACL 
method /proto.PartnerAPIService/GetPartnersForAPI is missing in the ACL 
method /proto.PartnerAPIService/GetRolesByPartnerForAPI is missing in the ACL 
method /proto.SFXDataSyncService/SyncGlobalAdvertiser is missing in the ACL 
4 out of all 175 interfaces are not configured yet
```

#### Available Options

```
--domain value, -d value   domain service folder name
--config value, -c value   access_control.yml relative path to domain service folder (default: "config/access_control.yml")
--package value, -p value  proto package relative path to domain service folder (default: "proto")
--help, -h                 show help
```
