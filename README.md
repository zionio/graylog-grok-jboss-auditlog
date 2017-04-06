[![license](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)](https://opensource.org/licenses/MIT)


# JBoss Audit Log GROK pattern for Graylog

(Tested on JBoss EAP 6.4)

**Pattern:**

	"name":"JBOSSAUDITLOG",
	"pattern":"(?s)%{TIMESTAMP_ISO8601:jboss_auditlog_timestamp} %{GREEDYDATA} \"type\" : %{QUOTEDSTRING:jboss_auditlog_type}%{GREEDYDATA} \"r/o\" : %{WORD:jboss_auditlog_ro}%{GREEDYDATA} \"booting\" : %{WORD:jboss_auditlog_booting}%{GREEDYDATA} \"version\" : %{QUOTEDSTRING:jboss_auditlog_version}%{GREEDYDATA} \"user\" : %{QUOTEDSTRING:jboss_auditlog_user}%{GREEDYDATA} \"domainUUID\" : %{QUOTEDSTRING:jboss_auditlog_domainuuid}%{GREEDYDATA} \"access\" : %{QUOTEDSTRING:jboss_auditlog_access}%{GREEDYDATA} \"remote-address\" : %{QUOTEDSTRING:jboss_auditlog_remote-address}%{GREEDYDATA} \"success\" : %{WORD:jboss_auditlog_success}%{GREEDYDATA} \"ops\" : \\[%{GREEDYDATA:jboss_auditlog_ops}\\]"

i.e.:

**message**

	2017-04-06 16:13:07 - { "type" : "core", "r/o" : false, "booting" : false, "version" : "6.4.13.GA", "user" : "user1", "domainUUID" : "aaaa-bbbb-cccc-dddd-eeee", "access" : "HTTP", "remote-address" : "127.0.0.1/127.0.0.1", "success" : true, "ops" : [{ "address" : [{"deployment" : "app1.ear"}], "operation" : "add", "runtime-name" : "app1.ear", "content" : [{"hash" : { "BYTES_VALUE" : "hash14234/ddsa" }}], "name" : "app1.ear", "enabled" : "true", "operation-headers" : {"access-mechanism" : "HTTP"} }] }

**fields**

	jboss_auditlog_access: HTTP
	jboss_auditlog_booting: false
	jboss_auditlog_domainuuid: aaaa-bbbb-cccc-dddd-eeee
	jboss_auditlog_ops: {
            "address" : [{"deployment" : "app1.ear"}],
            "operation" : "add",
            "runtime-name" : "app1.ear",
            "content" : [{"hash" : {
                "BYTES_VALUE" : "hash14234/ddsa"
            }}],
            "name" : "app1.ear",
            "enabled" : "true",
            "operation-headers" : {"access-mechanism" : "HTTP"}
        }
	jboss_auditlog_remote-address: 127.0.0.1/127.0.0.1
	jboss_auditlog_ro: false
	jboss_auditlog_success: true
	jboss_auditlog_timestamp: 2017-04-06 16:13:07
	jboss_auditlog_type: core
	jboss_auditlog_user: user1
	jboss_auditlog_version: 6.4.13.GA
