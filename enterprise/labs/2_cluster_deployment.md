```json
{
  "timestamp" : "2017-10-18T15:02:33.523Z",
  "clusters" : [ {
    "name" : "nicolobidotti",
    "version" : "CDH5",
    "services" : [ {
      "name" : "hive",
      "type" : "HIVE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "HIVEMETASTORE",
          "items" : [ {
            "name" : "hive_metastore_java_heapsize",
            "value" : "593494016"
          } ]
        }, {
          "roleType" : "HIVESERVER2",
          "items" : [ {
            "name" : "hiveserver2_java_heapsize",
            "value" : "593494016"
          }, {
            "name" : "hiveserver2_spark_driver_memory",
            "value" : "966367641"
          }, {
            "name" : "hiveserver2_spark_executor_cores",
            "value" : "4"
          }, {
            "name" : "hiveserver2_spark_executor_memory",
            "value" : "3433247539"
          }, {
            "name" : "hiveserver2_spark_yarn_driver_memory_overhead",
            "value" : "102"
          }, {
            "name" : "hiveserver2_spark_yarn_executor_memory_overhead",
            "value" : "577"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_metastore_database_host",
          "value" : "ip-172-31-5-172.eu-central-1.compute.internal"
        }, {
          "name" : "hive_metastore_database_password",
          "value" : "hive_password"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hive-GATEWAY-553e534e49afb1123562a05c750b071c",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-098b609c7571f241b"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-82dc72ed59d0701ccd52d6094513a18a",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0d023529513f2b8fc"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-a8be554d6a1da78282b8b1145885fd66",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0d4b501af1037406a"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-b7a52b74d46d7fa668677f933a5e79e6",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-07f38b0efa7142ede"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-HIVEMETASTORE-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "HIVEMETASTORE",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2tic41z279s97tclw5k7gjlqu"
          } ]
        }
      }, {
        "name" : "hive-HIVESERVER2-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "HIVESERVER2",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "62bzhj5nrcz4xztw8uhdh757f"
          } ]
        }
      } ],
      "displayName" : "Hive"
    }, {
      "name" : "zookeeper",
      "type" : "ZOOKEEPER",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "SERVER",
          "items" : [ {
            "name" : "dataDir",
            "value" : "/mnt/ssd0/zookeeper"
          }, {
            "name" : "dataLogDir",
            "value" : "/mnt/ssd0/zookeeper"
          } ]
        } ],
        "items" : [ ]
      },
      "roles" : [ {
        "name" : "zookeeper-SERVER-553e534e49afb1123562a05c750b071c",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-098b609c7571f241b"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "aorn3ahb1vv2mkw2h5sv0rihi"
          }, {
            "name" : "serverId",
            "value" : "1"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-82dc72ed59d0701ccd52d6094513a18a",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-0d023529513f2b8fc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "bajkhzqut9alw02ag4h54n43k"
          }, {
            "name" : "serverId",
            "value" : "2"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-b7a52b74d46d7fa668677f933a5e79e6",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-07f38b0efa7142ede"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "4rnap2hf76o4a264b19g8sl09"
          }, {
            "name" : "serverId",
            "value" : "3"
          } ]
        }
      } ],
      "displayName" : "ZooKeeper"
    }, {
      "name" : "hue",
      "type" : "HUE",
      "config" : {
        "roleTypeConfigs" : [ ],
        "items" : [ {
          "name" : "database_host",
          "value" : "ip-172-31-5-172.eu-central-1.compute.internal"
        }, {
          "name" : "database_password",
          "value" : "hue_password"
        }, {
          "name" : "database_type",
          "value" : "mysql"
        }, {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "hue_webhdfs",
          "value" : "hdfs-HTTPFS-a656ceefc15c3b5574cfadc23824ac33"
        }, {
          "name" : "oozie_service",
          "value" : "oozie"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hue-HUE_SERVER-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "HUE_SERVER",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "89n070xrnv7r9dm4p5zzs1wbi"
          }, {
            "name" : "secret_key",
            "value" : "EUQdqvfzUCEtg1O0LdTgXmFqy7FRN2"
          } ]
        }
      } ],
      "displayName" : "Hue"
    }, {
      "name" : "oozie",
      "type" : "OOZIE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "OOZIE_SERVER",
          "items" : [ {
            "name" : "oozie_database_host",
            "value" : "ip-172-31-5-172.eu-central-1.compute.internal"
          }, {
            "name" : "oozie_database_password",
            "value" : "oozie_password"
          }, {
            "name" : "oozie_database_type",
            "value" : "mysql"
          }, {
            "name" : "oozie_database_user",
            "value" : "oozie"
          }, {
            "name" : "oozie_java_heapsize",
            "value" : "593494016"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "oozie-OOZIE_SERVER-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "OOZIE_SERVER",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "f08t4heaasgar35cd3hzmb4o6"
          } ]
        }
      } ],
      "displayName" : "Oozie"
    }, {
      "name" : "yarn",
      "type" : "YARN",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "mapred_reduce_tasks",
            "value" : "8"
          }, {
            "name" : "mapred_submit_replication",
            "value" : "2"
          } ]
        }, {
          "roleType" : "JOBHISTORY",
          "items" : [ {
            "name" : "mr2_jobhistory_java_heapsize",
            "value" : "593494016"
          } ]
        }, {
          "roleType" : "NODEMANAGER",
          "items" : [ {
            "name" : "rm_cpu_shares",
            "value" : "1800"
          }, {
            "name" : "rm_io_weight",
            "value" : "900"
          }, {
            "name" : "yarn_nodemanager_heartbeat_interval_ms",
            "value" : "100"
          }, {
            "name" : "yarn_nodemanager_local_dirs",
            "value" : "/mnt/ssd0/yarn/nm,/mnt/ssd1/yarn/nm"
          }, {
            "name" : "yarn_nodemanager_log_dirs",
            "value" : "/mnt/yarn/container-logs"
          }, {
            "name" : "yarn_nodemanager_resource_cpu_vcores",
            "value" : "4"
          }, {
            "name" : "yarn_nodemanager_resource_memory_mb",
            "value" : "6144"
          } ]
        }, {
          "roleType" : "RESOURCEMANAGER",
          "items" : [ {
            "name" : "resource_manager_java_heapsize",
            "value" : "593494016"
          }, {
            "name" : "yarn_rm_bind_wildcard",
            "value" : "true"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_mb",
            "value" : "3608"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_vcores",
            "value" : "3"
          } ]
        } ],
        "items" : [ {
          "name" : "hdfs_service",
          "value" : "hdfs"
        }, {
          "name" : "rm_dirty",
          "value" : "true"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "90"
        }, {
          "name" : "yarn_service_cgroups",
          "value" : "false"
        }, {
          "name" : "yarn_service_lce_always",
          "value" : "false"
        }, {
          "name" : "zk_authorization_secret_key",
          "value" : "FCjCXqoKW28D2mS3QmEBnPWLyHKv9Y"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "yarn-JOBHISTORY-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "JOBHISTORY",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "4k1hag5usedjspigh13m4ns82"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-553e534e49afb1123562a05c750b071c",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-098b609c7571f241b"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "adgho10mus4ys47rejpqe12ug"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-82dc72ed59d0701ccd52d6094513a18a",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-0d023529513f2b8fc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "234stv1agyl100nt034kejwj"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-a8be554d6a1da78282b8b1145885fd66",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-0d4b501af1037406a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "cqt9uerq00159hcumh0r8n1nu"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-b7a52b74d46d7fa668677f933a5e79e6",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-07f38b0efa7142ede"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "1217jjkyu4tsg5gzir2kdk109"
          } ]
        }
      }, {
        "name" : "yarn-RESOURCEMANAGER-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "RESOURCEMANAGER",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ {
            "name" : "rm_id",
            "value" : "80"
          }, {
            "name" : "role_jceks_password",
            "value" : "9sdnblyac8l24kh9ilwutn8zj"
          } ]
        }
      } ],
      "displayName" : "YARN (MR2 Included)"
    }, {
      "name" : "hdfs",
      "type" : "HDFS",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "BALANCER",
          "items" : [ {
            "name" : "balancer_java_heapsize",
            "value" : "593494016"
          } ]
        }, {
          "roleType" : "DATANODE",
          "items" : [ {
            "name" : "datanode_java_heapsize",
            "value" : "1073741824"
          }, {
            "name" : "dfs_data_dir_list",
            "value" : "/mnt/ssd0/dfs/dn,/mnt/ssd1/dfs/dn"
          }, {
            "name" : "dfs_datanode_du_reserved",
            "value" : "3949091225"
          }, {
            "name" : "dfs_datanode_max_locked_memory",
            "value" : "2147483648"
          }, {
            "name" : "rm_cpu_shares",
            "value" : "200"
          }, {
            "name" : "rm_io_weight",
            "value" : "100"
          } ]
        }, {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "dfs_client_use_trash",
            "value" : "true"
          } ]
        }, {
          "roleType" : "JOURNALNODE",
          "items" : [ {
            "name" : "dfs_journalnode_edits_dir",
            "value" : "/mnt/ssd0/dfs/jn"
          } ]
        }, {
          "roleType" : "NAMENODE",
          "items" : [ {
            "name" : "dfs_name_dir_list",
            "value" : "/mnt/ssd0/dfs/nn"
          }, {
            "name" : "dfs_namenode_servicerpc_address",
            "value" : "8022"
          }, {
            "name" : "namenode_bind_wildcard",
            "value" : "true"
          } ]
        }, {
          "roleType" : "SECONDARYNAMENODE",
          "items" : [ {
            "name" : "fs_checkpoint_dir_list",
            "value" : "/mnt/ssd0/dfs/snn"
          } ]
        } ],
        "items" : [ {
          "name" : "dfs_ha_fencing_cloudera_manager_secret_key",
          "value" : "PMiXTCOlzlQ1BQPM1wztxrDmyTnPX6"
        }, {
          "name" : "dfs_ha_fencing_methods",
          "value" : "shell(true)"
        }, {
          "name" : "fc_authorization_secret_key",
          "value" : "FHl51tVszFa3938aUlO4kFsqeMJiZU"
        }, {
          "name" : "http_auth_signature_secret",
          "value" : "8szgTzuy5D7ZOmhkrrvOJ6FR8YgNEZ"
        }, {
          "name" : "rm_dirty",
          "value" : "true"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "10"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hdfs-BALANCER-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "BALANCER",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-DATANODE-553e534e49afb1123562a05c750b071c",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-098b609c7571f241b"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "a9edy0q0y0fdn7zgquvkqwoyl"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-82dc72ed59d0701ccd52d6094513a18a",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-0d023529513f2b8fc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "agpk9fhfmnuboui8xo1uu8kz9"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-a8be554d6a1da78282b8b1145885fd66",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-0d4b501af1037406a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "bf6v9lwe9slrylh86hm0gxc1k"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-b7a52b74d46d7fa668677f933a5e79e6",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-07f38b0efa7142ede"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "7eza5jfeu9rnkqm1auqmuvgat"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "9g1oyofk2whnwl4jwwk9hjycv"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-a8be554d6a1da78282b8b1145885fd66",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "i-0d4b501af1037406a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "78l38slpre8st3pnzx0d7sk1g"
          } ]
        }
      }, {
        "name" : "hdfs-GATEWAY-553e534e49afb1123562a05c750b071c",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-098b609c7571f241b"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-GATEWAY-82dc72ed59d0701ccd52d6094513a18a",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0d023529513f2b8fc"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-GATEWAY-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-GATEWAY-a8be554d6a1da78282b8b1145885fd66",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0d4b501af1037406a"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-GATEWAY-b7a52b74d46d7fa668677f933a5e79e6",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-07f38b0efa7142ede"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-HTTPFS-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "HTTPFS",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "k7g0sm5lf41es61ch3yt1axc"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-553e534e49afb1123562a05c750b071c",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "i-098b609c7571f241b"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "9nmqh3vendeiuya0d4i4vkasr"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "55jf4ni2vp5ejy1ohksuz2891"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-a8be554d6a1da78282b8b1145885fd66",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "i-0d4b501af1037406a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "ay5b0g0tub1o4oeec0w2nvqa7"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-a656ceefc15c3b5574cfadc23824ac33",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "i-09e2400beb088904d"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "nameservice1"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "nameservice1"
          }, {
            "name" : "namenode_id",
            "value" : "82"
          }, {
            "name" : "role_jceks_password",
            "value" : "5rdvcfy5u32luhy2brvxxcmu4"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-a8be554d6a1da78282b8b1145885fd66",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "i-0d4b501af1037406a"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "nameservice1"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "nameservice1"
          }, {
            "name" : "namenode_id",
            "value" : "93"
          }, {
            "name" : "role_jceks_password",
            "value" : "234r89kszg8ompt5lcyh4p51g"
          } ]
        }
      } ],
      "displayName" : "HDFS"
    } ]
  } ],
  "hosts" : [ {
    "hostId" : "i-0d023529513f2b8fc",
    "ipAddress" : "172.31.10.208",
    "hostname" : "ip-172-31-10-208.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-07f38b0efa7142ede",
    "ipAddress" : "172.31.12.159",
    "hostname" : "ip-172-31-12-159.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-098b609c7571f241b",
    "ipAddress" : "172.31.13.237",
    "hostname" : "ip-172-31-13-237.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-0d4b501af1037406a",
    "ipAddress" : "172.31.3.37",
    "hostname" : "ip-172-31-3-37.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-09e2400beb088904d",
    "ipAddress" : "172.31.5.172",
    "hostname" : "ip-172-31-5-172.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  } ],
  "users" : [ {
    "name" : "__cloudera_internal_user__mgmt-ACTIVITYMONITOR-a656ceefc15c3b5574cfadc23824ac33",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "ce5dd45747d5e015401dfdc53ffea72f3d083cb21c97d21230e95809325eb48d",
    "pwSalt" : -2065522581545321336,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-EVENTSERVER-a656ceefc15c3b5574cfadc23824ac33",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "62b703d3d840854decebc6701559c2ed8df9a035265c67fa2369eb91bee22b9e",
    "pwSalt" : -6835066073774732703,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-HOSTMONITOR-a656ceefc15c3b5574cfadc23824ac33",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "ce709654ecd5ac498867f09b45c2c56a4d3170d704675c4423df5a93bcac4ba5",
    "pwSalt" : 3036716362541023969,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-REPORTSMANAGER-a656ceefc15c3b5574cfadc23824ac33",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "70a91cd6a196794fe0344e2ba1371a3d15eced0a4ed82ebba70b668c94a6cb08",
    "pwSalt" : -72668268651592275,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-SERVICEMONITOR-a656ceefc15c3b5574cfadc23824ac33",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "024a88d2110994bcd1367b96d96ec5b03c3b1f4601c1f2c0d8a2d88b41beb726",
    "pwSalt" : 3917571955543641962,
    "pwLogin" : true
  }, {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ],
    "pwHash" : "48f04718a39511a71e801835e9bb07c4446d7f13729591d8d9caff37f297a895",
    "pwSalt" : -2109522725748678085,
    "pwLogin" : true
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ],
    "pwHash" : "84e85ec4f0a163775feb3896a44b41538e381011dbaf8161331f471d13b88d06",
    "pwSalt" : -1609640458297592469,
    "pwLogin" : true
  }, {
    "name" : "nicolobidotti",
    "roles" : [ "ROLE_ADMIN" ],
    "pwHash" : "3fc7e9d07468ad80e950212f4b82c2974e5d26561394389c6cc516a73c30a5ad",
    "pwSalt" : 9177351359242739446,
    "pwLogin" : true
  } ],
  "versionInfo" : {
    "version" : "5.8.3",
    "buildUser" : "jenkins",
    "buildTimestamp" : "20161019-1013",
    "gitHash" : "518f0d6d44abc87bc392646e4369a20c8192b7cf",
    "snapshot" : false
  },
  "managementService" : {
    "name" : "mgmt",
    "type" : "MGMT",
    "config" : {
      "roleTypeConfigs" : [ {
        "roleType" : "ACTIVITYMONITOR",
        "items" : [ {
          "name" : "firehose_database_host",
          "value" : "ip-172-31-5-172.eu-central-1.compute.internal"
        }, {
          "name" : "firehose_database_name",
          "value" : "amon"
        }, {
          "name" : "firehose_database_password",
          "value" : "amon_password"
        }, {
          "name" : "firehose_database_user",
          "value" : "amon"
        }, {
          "name" : "firehose_heapsize",
          "value" : "593494016"
        } ]
      }, {
        "roleType" : "EVENTSERVER",
        "items" : [ {
          "name" : "event_server_heapsize",
          "value" : "593494016"
        } ]
      }, {
        "roleType" : "HOSTMONITOR",
        "items" : [ {
          "name" : "firehose_heapsize",
          "value" : "593494016"
        }, {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "805306368"
        }, {
          "name" : "role_config_suppression_firehose_heap_size_validator",
          "value" : "true"
        }, {
          "name" : "role_config_suppression_firehose_non_java_memory_validator",
          "value" : "true"
        } ]
      }, {
        "roleType" : "REPORTSMANAGER",
        "items" : [ {
          "name" : "headlamp_database_host",
          "value" : "ip-172-31-5-172.eu-central-1.compute.internal"
        }, {
          "name" : "headlamp_database_name",
          "value" : "rman"
        }, {
          "name" : "headlamp_database_password",
          "value" : "rman_password"
        }, {
          "name" : "headlamp_database_user",
          "value" : "rman"
        }, {
          "name" : "headlamp_heapsize",
          "value" : "593494016"
        } ]
      }, {
        "roleType" : "SERVICEMONITOR",
        "items" : [ {
          "name" : "firehose_heapsize",
          "value" : "593494016"
        }, {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "805306368"
        }, {
          "name" : "role_config_suppression_firehose_heap_size_validator",
          "value" : "true"
        }, {
          "name" : "role_config_suppression_firehose_non_java_memory_validator",
          "value" : "true"
        } ]
      } ],
      "items" : [ ]
    },
    "roles" : [ {
      "name" : "mgmt-ACTIVITYMONITOR-a656ceefc15c3b5574cfadc23824ac33",
      "type" : "ACTIVITYMONITOR",
      "hostRef" : {
        "hostId" : "i-09e2400beb088904d"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "cmlqf2d89vvs8ja0gc6xx626p"
        } ]
      }
    }, {
      "name" : "mgmt-ALERTPUBLISHER-a656ceefc15c3b5574cfadc23824ac33",
      "type" : "ALERTPUBLISHER",
      "hostRef" : {
        "hostId" : "i-09e2400beb088904d"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "4ihyoggasmzih7cua8yx4hjzy"
        } ]
      }
    }, {
      "name" : "mgmt-EVENTSERVER-a656ceefc15c3b5574cfadc23824ac33",
      "type" : "EVENTSERVER",
      "hostRef" : {
        "hostId" : "i-09e2400beb088904d"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "aa2v0mtek1oucx27r4yikcr51"
        } ]
      }
    }, {
      "name" : "mgmt-HOSTMONITOR-a656ceefc15c3b5574cfadc23824ac33",
      "type" : "HOSTMONITOR",
      "hostRef" : {
        "hostId" : "i-09e2400beb088904d"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "19zlmw63rgs0x15nqvo0dcwua"
        } ]
      }
    }, {
      "name" : "mgmt-REPORTSMANAGER-a656ceefc15c3b5574cfadc23824ac33",
      "type" : "REPORTSMANAGER",
      "hostRef" : {
        "hostId" : "i-09e2400beb088904d"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "4xn4ktm5591s083w64otwqyce"
        } ]
      }
    }, {
      "name" : "mgmt-SERVICEMONITOR-a656ceefc15c3b5574cfadc23824ac33",
      "type" : "SERVICEMONITOR",
      "hostRef" : {
        "hostId" : "i-09e2400beb088904d"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "51xs2yizkajpqaypurdr8uy1f"
        } ]
      }
    } ],
    "displayName" : "Cloudera Management Service"
  },
  "managerSettings" : {
    "items" : [ {
      "name" : "CLUSTER_STATS_START",
      "value" : "10/26/2012 17:40"
    }, {
      "name" : "PUBLIC_CLOUD_STATUS",
      "value" : "ON_PUBLIC_CLOUD"
    }, {
      "name" : "REMOTE_PARCEL_REPO_URLS",
      "value" : "https://archive.cloudera.com/cdh5/parcels/5.8.3/,https://archive.cloudera.com/cdh4/parcels/latest/,https://archive.cloudera.com/impala/parcels/latest/,https://archive.cloudera.com/search/parcels/latest/,https://archive.cloudera.com/accumulo/parcels/1.4/,https://archive.cloudera.com/accumulo-c5/parcels/latest/,https://archive.cloudera.com/kafka/parcels/latest/,https://archive.cloudera.com/navigator-keytrustee5/parcels/latest/,https://archive.cloudera.com/spark/parcels/latest/,https://archive.cloudera.com/sqoop-connectors/parcels/latest/,http://localhost:80/cdh5.8.3/"
    } ]
  }
}
```