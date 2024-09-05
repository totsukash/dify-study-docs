## Version

- Dify: v0.7.2

## account_integrates

```
dify=# \d account_integrates
                              Table "public.account_integrates"
     Column      |            Type             | Collation | Nullable |       Default        
-----------------+-----------------------------+-----------+----------+----------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 account_id      | uuid                        |           | not null | 
 provider        | character varying(16)       |           | not null | 
 open_id         | character varying(255)      |           | not null | 
 encrypted_token | character varying(255)      |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "account_integrate_pkey" PRIMARY KEY, btree (id)
    "unique_account_provider" UNIQUE CONSTRAINT, btree (account_id, provider)
    "unique_provider_open_id" UNIQUE CONSTRAINT, btree (provider, open_id)
```

## accounts

```
dify=# \d accounts
                                        Table "public.accounts"
       Column       |            Type             | Collation | Nullable |           Default           
--------------------+-----------------------------+-----------+----------+-----------------------------
 id                 | uuid                        |           | not null | uuid_generate_v4()
 name               | character varying(255)      |           | not null | 
 email              | character varying(255)      |           | not null | 
 password           | character varying(255)      |           |          | 
 password_salt      | character varying(255)      |           |          | 
 avatar             | character varying(255)      |           |          | 
 interface_language | character varying(255)      |           |          | 
 interface_theme    | character varying(255)      |           |          | 
 timezone           | character varying(255)      |           |          | 
 last_login_at      | timestamp without time zone |           |          | 
 last_login_ip      | character varying(255)      |           |          | 
 status             | character varying(16)       |           | not null | 'active'::character varying
 initialized_at     | timestamp without time zone |           |          | 
 created_at         | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at         | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 last_active_at     | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "account_pkey" PRIMARY KEY, btree (id)
    "account_email_idx" btree (email)
```

## alembic_version

```
dify=# \d alembic_version
                    Table "public.alembic_version"
   Column    |         Type          | Collation | Nullable | Default 
-------------+-----------------------+-----------+----------+---------
 version_num | character varying(32) |           | not null | 
Indexes:
    "alembic_version_pkc" PRIMARY KEY, btree (version_num)
```

## api_based_extensions

```
dify=# \d alembic_version
                    Table "public.alembic_version"
   Column    |         Type          | Collation | Nullable | Default 
-------------+-----------------------+-----------+----------+---------
 version_num | character varying(32) |           | not null | 
Indexes:
    "alembic_version_pkc" PRIMARY KEY, btree (version_num)

dify=# \d api_based_extensions
                           Table "public.api_based_extensions"
    Column    |            Type             | Collation | Nullable |       Default        
--------------+-----------------------------+-----------+----------+----------------------
 id           | uuid                        |           | not null | uuid_generate_v4()
 tenant_id    | uuid                        |           | not null | 
 name         | character varying(255)      |           | not null | 
 api_endpoint | character varying(255)      |           | not null | 
 api_key      | text                        |           | not null | 
 created_at   | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "api_based_extension_pkey" PRIMARY KEY, btree (id)
    "api_based_extension_tenant_idx" btree (tenant_id)
```

## api_requests

```
dify=# \d api_requests
                               Table "public.api_requests"
    Column    |            Type             | Collation | Nullable |       Default        
--------------+-----------------------------+-----------+----------+----------------------
 id           | uuid                        |           | not null | uuid_generate_v4()
 tenant_id    | uuid                        |           | not null | 
 api_token_id | uuid                        |           | not null | 
 path         | character varying(255)      |           | not null | 
 request      | text                        |           |          | 
 response     | text                        |           |          | 
 ip           | character varying(255)      |           | not null | 
 created_at   | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "api_request_pkey" PRIMARY KEY, btree (id)
    "api_request_token_idx" btree (tenant_id, api_token_id)
```

## api_tokens

```
dify=# \d api_tokens
                                Table "public.api_tokens"
    Column    |            Type             | Collation | Nullable |       Default        
--------------+-----------------------------+-----------+----------+----------------------
 id           | uuid                        |           | not null | uuid_generate_v4()
 app_id       | uuid                        |           |          | 
 type         | character varying(16)       |           | not null | 
 token        | character varying(255)      |           | not null | 
 last_used_at | timestamp without time zone |           |          | 
 created_at   | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 tenant_id    | uuid                        |           |          | 
Indexes:
    "api_token_pkey" PRIMARY KEY, btree (id)
    "api_token_app_id_type_idx" btree (app_id, type)
    "api_token_tenant_idx" btree (tenant_id, type)
    "api_token_token_idx" btree (token, type)
```

## app_annotation_hit_histories

```
dify=# \d app_annotation_hit_histories
                           Table "public.app_annotation_hit_histories"
       Column        |            Type             | Collation | Nullable |       Default        
---------------------+-----------------------------+-----------+----------+----------------------
 id                  | uuid                        |           | not null | uuid_generate_v4()
 app_id              | uuid                        |           | not null | 
 annotation_id       | uuid                        |           | not null | 
 source              | text                        |           | not null | 
 question            | text                        |           | not null | 
 account_id          | uuid                        |           | not null | 
 created_at          | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 score               | double precision            |           | not null | 0
 message_id          | uuid                        |           | not null | 
 annotation_question | text                        |           | not null | 
 annotation_content  | text                        |           | not null | 
Indexes:
    "app_annotation_hit_histories_pkey" PRIMARY KEY, btree (id)
    "app_annotation_hit_histories_account_idx" btree (account_id)
    "app_annotation_hit_histories_annotation_idx" btree (annotation_id)
    "app_annotation_hit_histories_app_idx" btree (app_id)
    "app_annotation_hit_histories_message_idx" btree (message_id)
```

## app_annotation_settings

```
dify=# \d app_annotation_settings
                              Table "public.app_annotation_settings"
        Column         |            Type             | Collation | Nullable |       Default        
-----------------------+-----------------------------+-----------+----------+----------------------
 id                    | uuid                        |           | not null | uuid_generate_v4()
 app_id                | uuid                        |           | not null | 
 score_threshold       | double precision            |           | not null | 0
 collection_binding_id | uuid                        |           | not null | 
 created_user_id       | uuid                        |           | not null | 
 created_at            | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_user_id       | uuid                        |           | not null | 
 updated_at            | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "app_annotation_settings_pkey" PRIMARY KEY, btree (id)
    "app_annotation_settings_app_idx" btree (app_id)
```

## app_dataset_joins

```
dify=# \d app_dataset_joins
                           Table "public.app_dataset_joins"
   Column   |            Type             | Collation | Nullable |      Default       
------------+-----------------------------+-----------+----------+--------------------
 id         | uuid                        |           | not null | uuid_generate_v4()
 app_id     | uuid                        |           | not null | 
 dataset_id | uuid                        |           | not null | 
 created_at | timestamp without time zone |           | not null | CURRENT_TIMESTAMP
Indexes:
    "app_dataset_join_pkey" PRIMARY KEY, btree (id)
    "app_dataset_join_app_dataset_idx" btree (dataset_id, app_id)
```

## app_model_configs

```
dify=# \d app_model_configs
                                          Table "public.app_model_configs"
              Column              |            Type             | Collation | Nullable |           Default           
----------------------------------+-----------------------------+-----------+----------+-----------------------------
 id                               | uuid                        |           | not null | uuid_generate_v4()
 app_id                           | uuid                        |           | not null | 
 provider                         | character varying(255)      |           |          | 
 model_id                         | character varying(255)      |           |          | 
 configs                          | json                        |           |          | 
 created_at                       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at                       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 opening_statement                | text                        |           |          | 
 suggested_questions              | text                        |           |          | 
 suggested_questions_after_answer | text                        |           |          | 
 more_like_this                   | text                        |           |          | 
 model                            | text                        |           |          | 
 user_input_form                  | text                        |           |          | 
 pre_prompt                       | text                        |           |          | 
 agent_mode                       | text                        |           |          | 
 speech_to_text                   | text                        |           |          | 
 sensitive_word_avoidance         | text                        |           |          | 
 retriever_resource               | text                        |           |          | 
 dataset_query_variable           | character varying(255)      |           |          | 
 prompt_type                      | character varying(255)      |           | not null | 'simple'::character varying
 chat_prompt_config               | text                        |           |          | 
 completion_prompt_config         | text                        |           |          | 
 dataset_configs                  | text                        |           |          | 
 external_data_tools              | text                        |           |          | 
 file_upload                      | text                        |           |          | 
 text_to_speech                   | text                        |           |          | 
 created_by                       | uuid                        |           |          | 
 updated_by                       | uuid                        |           |          | 
Indexes:
    "app_model_config_pkey" PRIMARY KEY, btree (id)
    "app_app_id_idx" btree (app_id)
```

## apps

```
dify=# \d apps
                                          Table "public.apps"
       Column        |            Type             | Collation | Nullable |           Default           
---------------------+-----------------------------+-----------+----------+-----------------------------
 id                  | uuid                        |           | not null | uuid_generate_v4()
 tenant_id           | uuid                        |           | not null | 
 name                | character varying(255)      |           | not null | 
 mode                | character varying(255)      |           | not null | 
 icon                | character varying(255)      |           |          | 
 icon_background     | character varying(255)      |           |          | 
 app_model_config_id | uuid                        |           |          | 
 status              | character varying(255)      |           | not null | 'normal'::character varying
 enable_site         | boolean                     |           | not null | 
 enable_api          | boolean                     |           | not null | 
 api_rpm             | integer                     |           | not null | 0
 api_rph             | integer                     |           | not null | 0
 is_demo             | boolean                     |           | not null | false
 is_public           | boolean                     |           | not null | false
 created_at          | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at          | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 is_universal        | boolean                     |           | not null | false
 workflow_id         | uuid                        |           |          | 
 description         | text                        |           | not null | ''::character varying
 tracing             | text                        |           |          | 
 max_active_requests | integer                     |           |          | 
 icon_type           | character varying(255)      |           |          | 
 created_by          | uuid                        |           |          | 
 updated_by          | uuid                        |           |          | 
Indexes:
    "app_pkey" PRIMARY KEY, btree (id)
    "app_tenant_id_idx" btree (tenant_id)
Referenced by:
    TABLE "tool_published_apps" CONSTRAINT "tool_published_apps_app_id_fkey" FOREIGN KEY (app_id) REFERENCES apps(id)
```

## celery_taskmeta

```
dify=# \d celery_taskmeta
                                     Table "public.celery_taskmeta"
  Column   |            Type             | Collation | Nullable |                Default                
-----------+-----------------------------+-----------+----------+---------------------------------------
 id        | integer                     |           | not null | nextval('task_id_sequence'::regclass)
 task_id   | character varying(155)      |           |          | 
 status    | character varying(50)       |           |          | 
 result    | bytea                       |           |          | 
 date_done | timestamp without time zone |           |          | 
 traceback | text                        |           |          | 
 name      | character varying(155)      |           |          | 
 args      | bytea                       |           |          | 
 kwargs    | bytea                       |           |          | 
 worker    | character varying(155)      |           |          | 
 retries   | integer                     |           |          | 
 queue     | character varying(155)      |           |          | 
Indexes:
    "celery_taskmeta_pkey" PRIMARY KEY, btree (id)
    "celery_taskmeta_task_id_key" UNIQUE CONSTRAINT, btree (task_id)
```

## celery_tasksetmeta

```
dify=# \d celery_tasksetmeta
                                     Table "public.celery_tasksetmeta"
   Column   |            Type             | Collation | Nullable |                 Default                  
------------+-----------------------------+-----------+----------+------------------------------------------
 id         | integer                     |           | not null | nextval('taskset_id_sequence'::regclass)
 taskset_id | character varying(155)      |           |          | 
 result     | bytea                       |           |          | 
 date_done  | timestamp without time zone |           |          | 
Indexes:
    "celery_tasksetmeta_pkey" PRIMARY KEY, btree (id)
    "celery_tasksetmeta_taskset_id_key" UNIQUE CONSTRAINT, btree (taskset_id)
```

## conversations

```
dify=# \d conversations
                                     Table "public.conversations"
          Column           |            Type             | Collation | Nullable |       Default        
---------------------------+-----------------------------+-----------+----------+----------------------
 id                        | uuid                        |           | not null | uuid_generate_v4()
 app_id                    | uuid                        |           | not null | 
 app_model_config_id       | uuid                        |           |          | 
 model_provider            | character varying(255)      |           |          | 
 override_model_configs    | text                        |           |          | 
 model_id                  | character varying(255)      |           |          | 
 mode                      | character varying(255)      |           | not null | 
 name                      | character varying(255)      |           | not null | 
 summary                   | text                        |           |          | 
 inputs                    | json                        |           |          | 
 introduction              | text                        |           |          | 
 system_instruction        | text                        |           |          | 
 system_instruction_tokens | integer                     |           | not null | 0
 status                    | character varying(255)      |           | not null | 
 from_source               | character varying(255)      |           | not null | 
 from_end_user_id          | uuid                        |           |          | 
 from_account_id           | uuid                        |           |          | 
 read_at                   | timestamp without time zone |           |          | 
 read_account_id           | uuid                        |           |          | 
 created_at                | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at                | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 is_deleted                | boolean                     |           | not null | false
 invoke_from               | character varying(255)      |           |          | 
 dialogue_count            | integer                     |           | not null | 0
Indexes:
    "conversation_pkey" PRIMARY KEY, btree (id)
    "conversation_app_from_user_idx" btree (app_id, from_source, from_end_user_id)
```

## data_source_api_key_auth_bindings

```
dify=# \d data_source_api_key_auth_bindings
                    Table "public.data_source_api_key_auth_bindings"
   Column    |            Type             | Collation | Nullable |       Default        
-------------+-----------------------------+-----------+----------+----------------------
 id          | uuid                        |           | not null | uuid_generate_v4()
 tenant_id   | uuid                        |           | not null | 
 category    | character varying(255)      |           | not null | 
 provider    | character varying(255)      |           | not null | 
 credentials | text                        |           |          | 
 created_at  | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at  | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 disabled    | boolean                     |           |          | false
Indexes:
    "data_source_api_key_auth_binding_pkey" PRIMARY KEY, btree (id)
    "data_source_api_key_auth_binding_provider_idx" btree (provider)
    "data_source_api_key_auth_binding_tenant_id_idx" btree (tenant_id)
```

## data_source_oauth_bindings

```
dify=# \d data_source_oauth_bindings
                        Table "public.data_source_oauth_bindings"
    Column    |            Type             | Collation | Nullable |       Default        
--------------+-----------------------------+-----------+----------+----------------------
 id           | uuid                        |           | not null | uuid_generate_v4()
 tenant_id    | uuid                        |           | not null | 
 access_token | character varying(255)      |           | not null | 
 provider     | character varying(255)      |           | not null | 
 source_info  | jsonb                       |           | not null | 
 created_at   | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at   | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 disabled     | boolean                     |           |          | false
Indexes:
    "source_binding_pkey" PRIMARY KEY, btree (id)
    "source_binding_tenant_id_idx" btree (tenant_id)
    "source_info_idx" gin (source_info)
```

## dataset_collection_bindings

```
dify=# \d dataset_collection_bindings
                             Table "public.dataset_collection_bindings"
     Column      |            Type             | Collation | Nullable |           Default            
-----------------+-----------------------------+-----------+----------+------------------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 provider_name   | character varying(40)       |           | not null | 
 model_name      | character varying(255)      |           | not null | 
 collection_name | character varying(64)       |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 type            | character varying(40)       |           | not null | 'dataset'::character varying
Indexes:
    "dataset_collection_bindings_pkey" PRIMARY KEY, btree (id)
    "provider_model_name_idx" btree (provider_name, model_name)
```

## dataset_keyword_tables

```
dify=# \d dataset_keyword_tables
                              Table "public.dataset_keyword_tables"
      Column      |          Type          | Collation | Nullable |            Default            
------------------+------------------------+-----------+----------+-------------------------------
 id               | uuid                   |           | not null | uuid_generate_v4()
 dataset_id       | uuid                   |           | not null | 
 keyword_table    | text                   |           | not null | 
 data_source_type | character varying(255) |           | not null | 'database'::character varying
Indexes:
    "dataset_keyword_table_pkey" PRIMARY KEY, btree (id)
    "dataset_keyword_table_dataset_id_idx" btree (dataset_id)
    "dataset_keyword_tables_dataset_id_key" UNIQUE CONSTRAINT, btree (dataset_id)
```

## dataset_permissions

```
dify=# \d dataset_permissions
                             Table "public.dataset_permissions"
     Column     |            Type             | Collation | Nullable |       Default        
----------------+-----------------------------+-----------+----------+----------------------
 id             | uuid                        |           | not null | uuid_generate_v4()
 dataset_id     | uuid                        |           | not null | 
 account_id     | uuid                        |           | not null | 
 has_permission | boolean                     |           | not null | true
 created_at     | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 tenant_id      | uuid                        |           | not null | 
Indexes:
    "dataset_permission_pkey" PRIMARY KEY, btree (id)
    "idx_dataset_permissions_account_id" btree (account_id)
    "idx_dataset_permissions_dataset_id" btree (dataset_id)
    "idx_dataset_permissions_tenant_id" btree (tenant_id)
```

## dataset_process_rules

```
dify=# \d dataset_process_rules
                               Table "public.dataset_process_rules"
   Column   |            Type             | Collation | Nullable |            Default             
------------+-----------------------------+-----------+----------+--------------------------------
 id         | uuid                        |           | not null | uuid_generate_v4()
 dataset_id | uuid                        |           | not null | 
 mode       | character varying(255)      |           | not null | 'automatic'::character varying
 rules      | text                        |           |          | 
 created_by | uuid                        |           | not null | 
 created_at | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "dataset_process_rule_pkey" PRIMARY KEY, btree (id)
    "dataset_process_rule_dataset_id_idx" btree (dataset_id)
```

## dataset_queries

```
dify=# \d dataset_queries
                              Table "public.dataset_queries"
     Column      |            Type             | Collation | Nullable |      Default       
-----------------+-----------------------------+-----------+----------+--------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 dataset_id      | uuid                        |           | not null | 
 content         | text                        |           | not null | 
 source          | character varying(255)      |           | not null | 
 source_app_id   | uuid                        |           |          | 
 created_by_role | character varying           |           | not null | 
 created_by      | uuid                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP
Indexes:
    "dataset_query_pkey" PRIMARY KEY, btree (id)
    "dataset_query_dataset_id_idx" btree (dataset_id)
```

## dataset_retriever_resources

```
dify=# \d dataset_retriever_resources
                         Table "public.dataset_retriever_resources"
      Column      |            Type             | Collation | Nullable |      Default       
------------------+-----------------------------+-----------+----------+--------------------
 id               | uuid                        |           | not null | uuid_generate_v4()
 message_id       | uuid                        |           | not null | 
 position         | integer                     |           | not null | 
 dataset_id       | uuid                        |           | not null | 
 dataset_name     | text                        |           | not null | 
 document_id      | uuid                        |           | not null | 
 document_name    | text                        |           | not null | 
 data_source_type | text                        |           | not null | 
 segment_id       | uuid                        |           | not null | 
 score            | double precision            |           |          | 
 content          | text                        |           | not null | 
 hit_count        | integer                     |           |          | 
 word_count       | integer                     |           |          | 
 segment_position | integer                     |           |          | 
 index_node_hash  | text                        |           |          | 
 retriever_from   | text                        |           | not null | 
 created_by       | uuid                        |           | not null | 
 created_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP
Indexes:
    "dataset_retriever_resource_pkey" PRIMARY KEY, btree (id)
    "dataset_retriever_resource_message_id_idx" btree (message_id)
```

## datasets

```
dify=# \d datasets
                                                   Table "public.datasets"
          Column          |            Type             | Collation | Nullable |                   Default                   
--------------------------+-----------------------------+-----------+----------+---------------------------------------------
 id                       | uuid                        |           | not null | uuid_generate_v4()
 tenant_id                | uuid                        |           | not null | 
 name                     | character varying(255)      |           | not null | 
 description              | text                        |           |          | 
 provider                 | character varying(255)      |           | not null | 'vendor'::character varying
 permission               | character varying(255)      |           | not null | 'only_me'::character varying
 data_source_type         | character varying(255)      |           |          | 
 indexing_technique       | character varying(255)      |           |          | 
 index_struct             | text                        |           |          | 
 created_by               | uuid                        |           | not null | 
 created_at               | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_by               | uuid                        |           |          | 
 updated_at               | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 embedding_model          | character varying(255)      |           |          | 'text-embedding-ada-002'::character varying
 embedding_model_provider | character varying(255)      |           |          | 'openai'::character varying
 collection_binding_id    | uuid                        |           |          | 
 retrieval_model          | jsonb                       |           |          | 
Indexes:
    "dataset_pkey" PRIMARY KEY, btree (id)
    "dataset_tenant_idx" btree (tenant_id)
    "retrieval_model_idx" gin (retrieval_model)
```

## dify_setups

```
dify=# \d dify_setups
                              Table "public.dify_setups"
  Column  |            Type             | Collation | Nullable |       Default        
----------+-----------------------------+-----------+----------+----------------------
 version  | character varying(255)      |           | not null | 
 setup_at | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "dify_setup_pkey" PRIMARY KEY, btree (version)
```

## document_segments

```
dify=# \d document_segments
                                  Table "public.document_segments"
     Column      |            Type             | Collation | Nullable |           Default            
-----------------+-----------------------------+-----------+----------+------------------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 tenant_id       | uuid                        |           | not null | 
 dataset_id      | uuid                        |           | not null | 
 document_id     | uuid                        |           | not null | 
 position        | integer                     |           | not null | 
 content         | text                        |           | not null | 
 word_count      | integer                     |           | not null | 
 tokens          | integer                     |           | not null | 
 keywords        | json                        |           |          | 
 index_node_id   | character varying(255)      |           |          | 
 index_node_hash | character varying(255)      |           |          | 
 hit_count       | integer                     |           | not null | 
 enabled         | boolean                     |           | not null | true
 disabled_at     | timestamp without time zone |           |          | 
 disabled_by     | uuid                        |           |          | 
 status          | character varying(255)      |           | not null | 'waiting'::character varying
 created_by      | uuid                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 indexing_at     | timestamp without time zone |           |          | 
 completed_at    | timestamp without time zone |           |          | 
 error           | text                        |           |          | 
 stopped_at      | timestamp without time zone |           |          | 
 answer          | text                        |           |          | 
 updated_by      | uuid                        |           |          | 
 updated_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "document_segment_pkey" PRIMARY KEY, btree (id)
    "document_segment_dataset_id_idx" btree (dataset_id)
    "document_segment_dataset_node_idx" btree (dataset_id, index_node_id)
    "document_segment_document_id_idx" btree (document_id)
    "document_segment_tenant_dataset_idx" btree (dataset_id, tenant_id)
    "document_segment_tenant_document_idx" btree (document_id, tenant_id)
    "document_segment_tenant_idx" btree (tenant_id)
```

## documents

```
dify=# \d documents
                                            Table "public.documents"
         Column          |            Type             | Collation | Nullable |             Default             
-------------------------+-----------------------------+-----------+----------+---------------------------------
 id                      | uuid                        |           | not null | uuid_generate_v4()
 tenant_id               | uuid                        |           | not null | 
 dataset_id              | uuid                        |           | not null | 
 position                | integer                     |           | not null | 
 data_source_type        | character varying(255)      |           | not null | 
 data_source_info        | text                        |           |          | 
 dataset_process_rule_id | uuid                        |           |          | 
 batch                   | character varying(255)      |           | not null | 
 name                    | character varying(255)      |           | not null | 
 created_from            | character varying(255)      |           | not null | 
 created_by              | uuid                        |           | not null | 
 created_api_request_id  | uuid                        |           |          | 
 created_at              | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 processing_started_at   | timestamp without time zone |           |          | 
 file_id                 | text                        |           |          | 
 word_count              | integer                     |           |          | 
 parsing_completed_at    | timestamp without time zone |           |          | 
 cleaning_completed_at   | timestamp without time zone |           |          | 
 splitting_completed_at  | timestamp without time zone |           |          | 
 tokens                  | integer                     |           |          | 
 indexing_latency        | double precision            |           |          | 
 completed_at            | timestamp without time zone |           |          | 
 is_paused               | boolean                     |           |          | false
 paused_by               | uuid                        |           |          | 
 paused_at               | timestamp without time zone |           |          | 
 error                   | text                        |           |          | 
 stopped_at              | timestamp without time zone |           |          | 
 indexing_status         | character varying(255)      |           | not null | 'waiting'::character varying
 enabled                 | boolean                     |           | not null | true
 disabled_at             | timestamp without time zone |           |          | 
 disabled_by             | uuid                        |           |          | 
 archived                | boolean                     |           | not null | false
 archived_reason         | character varying(255)      |           |          | 
 archived_by             | uuid                        |           |          | 
 archived_at             | timestamp without time zone |           |          | 
 updated_at              | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 doc_type                | character varying(40)       |           |          | 
 doc_metadata            | json                        |           |          | 
 doc_form                | character varying(255)      |           | not null | 'text_model'::character varying
 doc_language            | character varying(255)      |           |          | 
Indexes:
    "document_pkey" PRIMARY KEY, btree (id)
    "document_dataset_id_idx" btree (dataset_id)
```

## embeddings

```
dify-# \d embeddings
                                            Table "public.embeddings"
    Column     |            Type             | Collation | Nullable |                   Default                   
---------------+-----------------------------+-----------+----------+---------------------------------------------
 id            | uuid                        |           | not null | uuid_generate_v4()
 hash          | character varying(64)       |           | not null | 
 embedding     | bytea                       |           | not null | 
 created_at    | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 model_name    | character varying(255)      |           | not null | 'text-embedding-ada-002'::character varying
 provider_name | character varying(255)      |           | not null | ''::character varying
Indexes:
    "embedding_pkey" PRIMARY KEY, btree (id)
    "created_at_idx" btree (created_at)
    "embedding_hash_idx" UNIQUE CONSTRAINT, btree (model_name, hash, provider_name)
```

## end_users

```
dify-# \d end_users
                                   Table "public.end_users"
      Column      |            Type             | Collation | Nullable |       Default        
------------------+-----------------------------+-----------+----------+----------------------
 id               | uuid                        |           | not null | uuid_generate_v4()
 tenant_id        | uuid                        |           | not null | 
 app_id           | uuid                        |           |          | 
 type             | character varying(255)      |           | not null | 
 external_user_id | character varying(255)      |           |          | 
 name             | character varying(255)      |           |          | 
 is_anonymous     | boolean                     |           | not null | true
 session_id       | character varying(255)      |           | not null | 
 created_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "end_user_pkey" PRIMARY KEY, btree (id)
    "end_user_session_id_idx" btree (session_id, type)
    "end_user_tenant_session_id_idx" btree (tenant_id, session_id, type)
```

## installed_apps

```
dify-# \d installed_apps
                                  Table "public.installed_apps"
       Column        |            Type             | Collation | Nullable |       Default        
---------------------+-----------------------------+-----------+----------+----------------------
 id                  | uuid                        |           | not null | uuid_generate_v4()
 tenant_id           | uuid                        |           | not null | 
 app_id              | uuid                        |           | not null | 
 app_owner_tenant_id | uuid                        |           | not null | 
 position            | integer                     |           | not null | 
 is_pinned           | boolean                     |           | not null | false
 last_used_at        | timestamp without time zone |           |          | 
 created_at          | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "installed_app_pkey" PRIMARY KEY, btree (id)
    "installed_app_app_id_idx" btree (app_id)
    "installed_app_tenant_id_idx" btree (tenant_id)
    "unique_tenant_app" UNIQUE CONSTRAINT, btree (tenant_id, app_id)
```

## invitation_codes

```
dify-# \d invitation_codes
                                            Table "public.invitation_codes"
       Column       |            Type             | Collation | Nullable |                   Default                    
--------------------+-----------------------------+-----------+----------+----------------------------------------------
 id                 | integer                     |           | not null | nextval('invitation_codes_id_seq'::regclass)
 batch              | character varying(255)      |           | not null | 
 code               | character varying(32)       |           | not null | 
 status             | character varying(16)       |           | not null | 'unused'::character varying
 used_at            | timestamp without time zone |           |          | 
 used_by_tenant_id  | uuid                        |           |          | 
 used_by_account_id | uuid                        |           |          | 
 deprecated_at      | timestamp without time zone |           |          | 
 created_at         | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "invitation_code_pkey" PRIMARY KEY, btree (id)
    "invitation_codes_batch_idx" btree (batch)
    "invitation_codes_code_idx" btree (code, status)
```

## invitation_codes_id_seq

```
dify-# \d invitation_codes_id_seq
              Sequence "public.invitation_codes_id_seq"
  Type   | Start | Minimum |  Maximum   | Increment | Cycles? | Cache 
---------+-------+---------+------------+-----------+---------+-------
 integer |     1 |       1 | 2147483647 |         1 | no      |     1
Owned by: public.invitation_codes.id
```

## load_balancing_model_configs

```
dify-# \d load_balancing_model_configs
                         Table "public.load_balancing_model_configs"
      Column      |            Type             | Collation | Nullable |       Default        
------------------+-----------------------------+-----------+----------+----------------------
 id               | uuid                        |           | not null | uuid_generate_v4()
 tenant_id        | uuid                        |           | not null | 
 provider_name    | character varying(255)      |           | not null | 
 model_name       | character varying(255)      |           | not null | 
 model_type       | character varying(40)       |           | not null | 
 name             | character varying(255)      |           | not null | 
 encrypted_config | text                        |           |          | 
 enabled          | boolean                     |           | not null | true
 created_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "load_balancing_model_config_pkey" PRIMARY KEY, btree (id)
    "load_balancing_model_config_tenant_provider_model_idx" btree (tenant_id, provider_name, model_type)
```

## message_agent_thoughts

```
dify-# \d message_agent_thoughts
                            Table "public.message_agent_thoughts"
       Column       |            Type             | Collation | Nullable |      Default       
--------------------+-----------------------------+-----------+----------+--------------------
 id                 | uuid                        |           | not null | uuid_generate_v4()
 message_id         | uuid                        |           | not null | 
 message_chain_id   | uuid                        |           |          | 
 position           | integer                     |           | not null | 
 thought            | text                        |           |          | 
 tool               | text                        |           |          | 
 tool_input         | text                        |           |          | 
 observation        | text                        |           |          | 
 tool_process_data  | text                        |           |          | 
 message            | text                        |           |          | 
 message_token      | integer                     |           |          | 
 message_unit_price | numeric                     |           |          | 
 answer             | text                        |           |          | 
 answer_token       | integer                     |           |          | 
 answer_unit_price  | numeric                     |           |          | 
 tokens             | integer                     |           |          | 
 total_price        | numeric                     |           |          | 
 currency           | character varying           |           |          | 
 latency            | double precision            |           |          | 
 created_by_role    | character varying           |           | not null | 
 created_by         | uuid                        |           | not null | 
 created_at         | timestamp without time zone |           | not null | CURRENT_TIMESTAMP
 message_price_unit | numeric(10,7)               |           | not null | 0.001
 answer_price_unit  | numeric(10,7)               |           | not null | 0.001
 message_files      | text                        |           |          | 
 tool_labels_str    | text                        |           | not null | '{}'::text
 tool_meta_str      | text                        |           | not null | '{}'::text
Indexes:
    "message_agent_thought_pkey" PRIMARY KEY, btree (id)
    "message_agent_thought_message_chain_id_idx" btree (message_chain_id)
    "message_agent_thought_message_id_idx" btree (message_id)
```

## message_annotations

```
dify-# \d message_annotations
                             Table "public.message_annotations"
     Column      |            Type             | Collation | Nullable |       Default        
-----------------+-----------------------------+-----------+----------+----------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 app_id          | uuid                        |           | not null | 
 conversation_id | uuid                        |           |          | 
 message_id      | uuid                        |           |          | 
 content         | text                        |           | not null | 
 account_id      | uuid                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 question        | text                        |           |          | 
 hit_count       | integer                     |           | not null | 0
Indexes:
    "message_annotation_pkey" PRIMARY KEY, btree (id)
    "message_annotation_app_idx" btree (app_id)
    "message_annotation_conversation_idx" btree (conversation_id)
    "message_annotation_message_idx" btree (message_id)
```

## message_chains

```
dify-# \d message_chains
                            Table "public.message_chains"
   Column   |            Type             | Collation | Nullable |      Default       
------------+-----------------------------+-----------+----------+--------------------
 id         | uuid                        |           | not null | uuid_generate_v4()
 message_id | uuid                        |           | not null | 
 type       | character varying(255)      |           | not null | 
 input      | text                        |           |          | 
 output     | text                        |           |          | 
 created_at | timestamp without time zone |           | not null | CURRENT_TIMESTAMP
Indexes:
    "message_chain_pkey" PRIMARY KEY, btree (id)
    "message_chain_message_id_idx" btree (message_id)
```

## message_feedbacks

```
dify-# \d message_feedbacks
                               Table "public.message_feedbacks"
      Column      |            Type             | Collation | Nullable |       Default        
------------------+-----------------------------+-----------+----------+----------------------
 id               | uuid                        |           | not null | uuid_generate_v4()
 app_id           | uuid                        |           | not null | 
 conversation_id  | uuid                        |           | not null | 
 message_id       | uuid                        |           | not null | 
 rating           | character varying(255)      |           | not null | 
 content          | text                        |           |          | 
 from_source      | character varying(255)      |           | not null | 
 from_end_user_id | uuid                        |           |          | 
 from_account_id  | uuid                        |           |          | 
 created_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "message_feedback_pkey" PRIMARY KEY, btree (id)
    "message_feedback_app_idx" btree (app_id)
    "message_feedback_conversation_idx" btree (conversation_id, from_source, rating)
    "message_feedback_message_idx" btree (message_id, from_source)
```

## message_files

```
dify-# \d message_files
                                Table "public.message_files"
     Column      |            Type             | Collation | Nullable |       Default        
-----------------+-----------------------------+-----------+----------+----------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 message_id      | uuid                        |           | not null | 
 type            | character varying(255)      |           | not null | 
 transfer_method | character varying(255)      |           | not null | 
 url             | text                        |           |          | 
 upload_file_id  | uuid                        |           |          | 
 created_by_role | character varying(255)      |           | not null | 
 created_by      | uuid                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 belongs_to      | character varying(255)      |           |          | 
Indexes:
    "message_file_pkey" PRIMARY KEY, btree (id)
    "message_file_created_by_idx" btree (created_by)
    "message_file_message_idx" btree (message_id)
```

## messages

```
dify-# \d messages
                                           Table "public.messages"
          Column           |            Type             | Collation | Nullable |           Default           
---------------------------+-----------------------------+-----------+----------+-----------------------------
 id                        | uuid                        |           | not null | uuid_generate_v4()
 app_id                    | uuid                        |           | not null | 
 model_provider            | character varying(255)      |           |          | 
 model_id                  | character varying(255)      |           |          | 
 override_model_configs    | text                        |           |          | 
 conversation_id           | uuid                        |           | not null | 
 inputs                    | json                        |           |          | 
 query                     | text                        |           | not null | 
 message                   | json                        |           | not null | 
 message_tokens            | integer                     |           | not null | 0
 message_unit_price        | numeric(10,4)               |           | not null | 
 answer                    | text                        |           | not null | 
 answer_tokens             | integer                     |           | not null | 0
 answer_unit_price         | numeric(10,4)               |           | not null | 
 provider_response_latency | double precision            |           | not null | 0
 total_price               | numeric(10,7)               |           |          | 
 currency                  | character varying(255)      |           | not null | 
 from_source               | character varying(255)      |           | not null | 
 from_end_user_id          | uuid                        |           |          | 
 from_account_id           | uuid                        |           |          | 
 created_at                | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at                | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 agent_based               | boolean                     |           | not null | false
 message_price_unit        | numeric(10,7)               |           | not null | 0.001
 answer_price_unit         | numeric(10,7)               |           | not null | 0.001
 workflow_run_id           | uuid                        |           |          | 
 status                    | character varying(255)      |           | not null | 'normal'::character varying
 error                     | text                        |           |          | 
 message_metadata          | text                        |           |          | 
 invoke_from               | character varying(255)      |           |          | 
Indexes:
    "message_pkey" PRIMARY KEY, btree (id)
    "message_account_idx" btree (app_id, from_source, from_account_id)
    "message_app_id_idx" btree (app_id, created_at)
    "message_conversation_id_idx" btree (conversation_id)
    "message_end_user_idx" btree (app_id, from_source, from_end_user_id)
    "message_workflow_run_id_idx" btree (conversation_id, workflow_run_id)
```

## operation_logs

```
dify-# \d operation_logs
                             Table "public.operation_logs"
   Column   |            Type             | Collation | Nullable |       Default        
------------+-----------------------------+-----------+----------+----------------------
 id         | uuid                        |           | not null | uuid_generate_v4()
 tenant_id  | uuid                        |           | not null | 
 account_id | uuid                        |           | not null | 
 action     | character varying(255)      |           | not null | 
 content    | json                        |           |          | 
 created_at | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 created_ip | character varying(255)      |           | not null | 
 updated_at | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "operation_log_pkey" PRIMARY KEY, btree (id)
    "operation_log_account_action_idx" btree (tenant_id, account_id, action)
```

## pinned_conversations

```
dify-# \d pinned_conversations
                                 Table "public.pinned_conversations"
     Column      |            Type             | Collation | Nullable |            Default            
-----------------+-----------------------------+-----------+----------+-------------------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 app_id          | uuid                        |           | not null | 
 conversation_id | uuid                        |           | not null | 
 created_by      | uuid                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 created_by_role | character varying(255)      |           | not null | 'end_user'::character varying
Indexes:
    "pinned_conversation_pkey" PRIMARY KEY, btree (id)
    "pinned_conversation_conversation_idx" btree (app_id, conversation_id, created_by_role, created_by)
```

## provider_model_settings

```
dify-# \d provider_model_settings
                               Table "public.provider_model_settings"
         Column         |            Type             | Collation | Nullable |       Default        
------------------------+-----------------------------+-----------+----------+----------------------
 id                     | uuid                        |           | not null | uuid_generate_v4()
 tenant_id              | uuid                        |           | not null | 
 provider_name          | character varying(255)      |           | not null | 
 model_name             | character varying(255)      |           | not null | 
 model_type             | character varying(40)       |           | not null | 
 enabled                | boolean                     |           | not null | true
 load_balancing_enabled | boolean                     |           | not null | false
 created_at             | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at             | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "provider_model_setting_pkey" PRIMARY KEY, btree (id)
    "provider_model_setting_tenant_provider_model_idx" btree (tenant_id, provider_name, model_type)
```

## provider_models

```
dify-# \d provider_models
                                Table "public.provider_models"
      Column      |            Type             | Collation | Nullable |       Default        
------------------+-----------------------------+-----------+----------+----------------------
 id               | uuid                        |           | not null | uuid_generate_v4()
 tenant_id        | uuid                        |           | not null | 
 provider_name    | character varying(255)      |           | not null | 
 model_name       | character varying(255)      |           | not null | 
 model_type       | character varying(40)       |           | not null | 
 encrypted_config | text                        |           |          | 
 is_valid         | boolean                     |           | not null | false
 created_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "provider_model_pkey" PRIMARY KEY, btree (id)
    "provider_model_tenant_id_provider_idx" btree (tenant_id, provider_name)
    "unique_provider_model_name" UNIQUE CONSTRAINT, btree (tenant_id, provider_name, model_name, model_type)
```

## provider_orders

```
dify-# \d provider_orders
                                     Table "public.provider_orders"
       Column       |            Type             | Collation | Nullable |            Default            
--------------------+-----------------------------+-----------+----------+-------------------------------
 id                 | uuid                        |           | not null | uuid_generate_v4()
 tenant_id          | uuid                        |           | not null | 
 provider_name      | character varying(255)      |           | not null | 
 account_id         | uuid                        |           | not null | 
 payment_product_id | character varying(191)      |           | not null | 
 payment_id         | character varying(191)      |           |          | 
 transaction_id     | character varying(191)      |           |          | 
 quantity           | integer                     |           | not null | 1
 currency           | character varying(40)       |           |          | 
 total_amount       | integer                     |           |          | 
 payment_status     | character varying(40)       |           | not null | 'wait_pay'::character varying
 paid_at            | timestamp without time zone |           |          | 
 pay_failed_at      | timestamp without time zone |           |          | 
 refunded_at        | timestamp without time zone |           |          | 
 created_at         | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at         | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "provider_order_pkey" PRIMARY KEY, btree (id)
    "provider_order_tenant_provider_idx" btree (tenant_id, provider_name)
```

## providers

```
dify-# \d providers
                                      Table "public.providers"
      Column      |            Type             | Collation | Nullable |           Default           
------------------+-----------------------------+-----------+----------+-----------------------------
 id               | uuid                        |           | not null | uuid_generate_v4()
 tenant_id        | uuid                        |           | not null | 
 provider_name    | character varying(255)      |           | not null | 
 provider_type    | character varying(40)       |           | not null | 'custom'::character varying
 encrypted_config | text                        |           |          | 
 is_valid         | boolean                     |           | not null | false
 last_used        | timestamp without time zone |           |          | 
 quota_type       | character varying(40)       |           |          | ''::character varying
 quota_limit      | bigint                      |           |          | 
 quota_used       | bigint                      |           |          | 
 created_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at       | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "provider_pkey" PRIMARY KEY, btree (id)
    "provider_tenant_id_provider_idx" btree (tenant_id, provider_name)
    "unique_provider_name_type_quota" UNIQUE CONSTRAINT, btree (tenant_id, provider_name, provider_type, quota_type)
```

## recommended_apps

```
dify-# \d recommended_apps
                                   Table "public.recommended_apps"
      Column       |            Type             | Collation | Nullable |          Default           
-------------------+-----------------------------+-----------+----------+----------------------------
 id                | uuid                        |           | not null | uuid_generate_v4()
 app_id            | uuid                        |           | not null | 
 description       | json                        |           | not null | 
 copyright         | character varying(255)      |           | not null | 
 privacy_policy    | character varying(255)      |           | not null | 
 category          | character varying(255)      |           | not null | 
 position          | integer                     |           | not null | 
 is_listed         | boolean                     |           | not null | 
 install_count     | integer                     |           | not null | 
 created_at        | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at        | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 language          | character varying(255)      |           | not null | 'en-US'::character varying
 custom_disclaimer | character varying(255)      |           |          | 
Indexes:
    "recommended_app_pkey" PRIMARY KEY, btree (id)
    "recommended_app_app_id_idx" btree (app_id)
    "recommended_app_is_listed_idx" btree (is_listed, language)
```

## saved_messages

```
dify-# \d saved_messages
                                    Table "public.saved_messages"
     Column      |            Type             | Collation | Nullable |            Default            
-----------------+-----------------------------+-----------+----------+-------------------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 app_id          | uuid                        |           | not null | 
 message_id      | uuid                        |           | not null | 
 created_by      | uuid                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 created_by_role | character varying(255)      |           | not null | 'end_user'::character varying
Indexes:
    "saved_message_pkey" PRIMARY KEY, btree (id)
    "saved_message_message_idx" btree (app_id, message_id, created_by_role, created_by)
```

## sites

```
dify-# \d sites
                                             Table "public.sites"
          Column           |            Type             | Collation | Nullable |           Default           
---------------------------+-----------------------------+-----------+----------+-----------------------------
 id                        | uuid                        |           | not null | uuid_generate_v4()
 app_id                    | uuid                        |           | not null | 
 title                     | character varying(255)      |           | not null | 
 icon                      | character varying(255)      |           |          | 
 icon_background           | character varying(255)      |           |          | 
 description               | text                        |           |          | 
 default_language          | character varying(255)      |           | not null | 
 copyright                 | character varying(255)      |           |          | 
 privacy_policy            | character varying(255)      |           |          | 
 customize_domain          | character varying(255)      |           |          | 
 customize_token_strategy  | character varying(255)      |           | not null | 
 prompt_public             | boolean                     |           | not null | false
 status                    | character varying(255)      |           | not null | 'normal'::character varying
 created_at                | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at                | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 code                      | character varying(255)      |           |          | 
 custom_disclaimer         | character varying(255)      |           |          | 
 show_workflow_steps       | boolean                     |           | not null | true
 chat_color_theme          | character varying(255)      |           |          | 
 chat_color_theme_inverted | boolean                     |           | not null | false
 icon_type                 | character varying(255)      |           |          | 
 created_by                | uuid                        |           |          | 
 updated_by                | uuid                        |           |          | 
Indexes:
    "site_pkey" PRIMARY KEY, btree (id)
    "site_app_id_idx" btree (app_id)
    "site_code_idx" btree (code, status)
```

## tag_bindings

```
dify-# \d tag_bindings
                              Table "public.tag_bindings"
   Column   |            Type             | Collation | Nullable |       Default        
------------+-----------------------------+-----------+----------+----------------------
 id         | uuid                        |           | not null | uuid_generate_v4()
 tenant_id  | uuid                        |           |          | 
 tag_id     | uuid                        |           |          | 
 target_id  | uuid                        |           |          | 
 created_by | uuid                        |           | not null | 
 created_at | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "tag_binding_pkey" PRIMARY KEY, btree (id)
    "tag_bind_tag_id_idx" btree (tag_id)
    "tag_bind_target_id_idx" btree (target_id)
```

## tags

```
dify-# \d tags
                                  Table "public.tags"
   Column   |            Type             | Collation | Nullable |       Default        
------------+-----------------------------+-----------+----------+----------------------
 id         | uuid                        |           | not null | uuid_generate_v4()
 tenant_id  | uuid                        |           |          | 
 type       | character varying(16)       |           | not null | 
 name       | character varying(255)      |           | not null | 
 created_by | uuid                        |           | not null | 
 created_at | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "tag_pkey" PRIMARY KEY, btree (id)
    "tag_name_idx" btree (name)
    "tag_type_idx" btree (type)
```

## task_id_sequence

```
dify-# \d task_id_sequence
                      Sequence "public.task_id_sequence"
  Type  | Start | Minimum |       Maximum       | Increment | Cycles? | Cache 
--------+-------+---------+---------------------+-----------+---------+-------
 bigint |     1 |       1 | 9223372036854775807 |         1 | no      |     1
```

## taskset_id_sequence

```
dify-# \d taskset_id_sequence
                    Sequence "public.taskset_id_sequence"
  Type  | Start | Minimum |       Maximum       | Increment | Cycles? | Cache 
--------+-------+---------+---------------------+-----------+---------+-------
 bigint |     1 |       1 | 9223372036854775807 |         1 | no      |     1
```

## tenant_account_joins

```
dify-# \d tenant_account_joins
                              Table "public.tenant_account_joins"
   Column   |            Type             | Collation | Nullable |           Default           
------------+-----------------------------+-----------+----------+-----------------------------
 id         | uuid                        |           | not null | uuid_generate_v4()
 tenant_id  | uuid                        |           | not null | 
 account_id | uuid                        |           | not null | 
 role       | character varying(16)       |           | not null | 'normal'::character varying
 invited_by | uuid                        |           |          | 
 created_at | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 current    | boolean                     |           | not null | false
Indexes:
    "tenant_account_join_pkey" PRIMARY KEY, btree (id)
    "tenant_account_join_account_id_idx" btree (account_id)
    "tenant_account_join_tenant_id_idx" btree (tenant_id)
    "unique_tenant_account_join" UNIQUE CONSTRAINT, btree (tenant_id, account_id)
```

## tenant_default_models

```
dify-# \d tenant_default_models
                           Table "public.tenant_default_models"
    Column     |            Type             | Collation | Nullable |       Default        
---------------+-----------------------------+-----------+----------+----------------------
 id            | uuid                        |           | not null | uuid_generate_v4()
 tenant_id     | uuid                        |           | not null | 
 provider_name | character varying(255)      |           | not null | 
 model_name    | character varying(255)      |           | not null | 
 model_type    | character varying(40)       |           | not null | 
 created_at    | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at    | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "tenant_default_model_pkey" PRIMARY KEY, btree (id)
    "tenant_default_model_tenant_id_provider_type_idx" btree (tenant_id, provider_name, model_type)
```

## tenant_preferred_model_providers

```
dify-# \d tenant_preferred_model_providers
                           Table "public.tenant_preferred_model_providers"
         Column          |            Type             | Collation | Nullable |       Default        
-------------------------+-----------------------------+-----------+----------+----------------------
 id                      | uuid                        |           | not null | uuid_generate_v4()
 tenant_id               | uuid                        |           | not null | 
 provider_name           | character varying(255)      |           | not null | 
 preferred_provider_type | character varying(40)       |           | not null | 
 created_at              | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at              | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "tenant_preferred_model_provider_pkey" PRIMARY KEY, btree (id)
    "tenant_preferred_model_provider_tenant_provider_idx" btree (tenant_id, provider_name)
```

## tenants

```
dify-# \d tenants
                                        Table "public.tenants"
       Column       |            Type             | Collation | Nullable |           Default           
--------------------+-----------------------------+-----------+----------+-----------------------------
 id                 | uuid                        |           | not null | uuid_generate_v4()
 name               | character varying(255)      |           | not null | 
 encrypt_public_key | text                        |           |          | 
 plan               | character varying(255)      |           | not null | 'basic'::character varying
 status             | character varying(255)      |           | not null | 'normal'::character varying
 created_at         | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at         | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 custom_config      | text                        |           |          | 
Indexes:
    "tenant_pkey" PRIMARY KEY, btree (id)
```

## tool_api_providers

```
dify-# \d tool_api_providers
                               Table "public.tool_api_providers"
      Column       |            Type             | Collation | Nullable |       Default        
-------------------+-----------------------------+-----------+----------+----------------------
 id                | uuid                        |           | not null | uuid_generate_v4()
 name              | character varying(40)       |           | not null | 
 schema            | text                        |           | not null | 
 schema_type_str   | character varying(40)       |           | not null | 
 user_id           | uuid                        |           | not null | 
 tenant_id         | uuid                        |           | not null | 
 tools_str         | text                        |           | not null | 
 icon              | character varying(255)      |           | not null | 
 credentials_str   | text                        |           | not null | 
 description       | text                        |           | not null | 
 created_at        | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at        | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 privacy_policy    | character varying(255)      |           |          | 
 custom_disclaimer | character varying(255)      |           |          | 
Indexes:
    "tool_api_provider_pkey" PRIMARY KEY, btree (id)
    "unique_api_tool_provider" UNIQUE CONSTRAINT, btree (name, tenant_id)
```

## tool_builtin_providers

```
dify-# \d tool_builtin_providers
                               Table "public.tool_builtin_providers"
        Column         |            Type             | Collation | Nullable |       Default        
-----------------------+-----------------------------+-----------+----------+----------------------
 id                    | uuid                        |           | not null | uuid_generate_v4()
 tenant_id             | uuid                        |           |          | 
 user_id               | uuid                        |           | not null | 
 provider              | character varying(40)       |           | not null | 
 encrypted_credentials | text                        |           |          | 
 created_at            | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at            | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "tool_builtin_provider_pkey" PRIMARY KEY, btree (id)
    "unique_builtin_tool_provider" UNIQUE CONSTRAINT, btree (tenant_id, provider)
```

## tool_conversation_variables

```
dify-# \d tool_conversation_variables
                         Table "public.tool_conversation_variables"
     Column      |            Type             | Collation | Nullable |       Default        
-----------------+-----------------------------+-----------+----------+----------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 user_id         | uuid                        |           | not null | 
 tenant_id       | uuid                        |           | not null | 
 conversation_id | uuid                        |           | not null | 
 variables_str   | text                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "tool_conversation_variables_pkey" PRIMARY KEY, btree (id)
    "conversation_id_idx" btree (conversation_id)
    "user_id_idx" btree (user_id)

```

## tool_files

```
dify-# \d tool_files
                               Table "public.tool_files"
     Column      |          Type           | Collation | Nullable |      Default       
-----------------+-------------------------+-----------+----------+--------------------
 id              | uuid                    |           | not null | uuid_generate_v4()
 user_id         | uuid                    |           | not null | 
 tenant_id       | uuid                    |           | not null | 
 conversation_id | uuid                    |           |          | 
 file_key        | character varying(255)  |           | not null | 
 mimetype        | character varying(255)  |           | not null | 
 original_url    | character varying(2048) |           |          | 
Indexes:
    "tool_file_pkey" PRIMARY KEY, btree (id)
    "tool_file_conversation_id_idx" btree (conversation_id)
```

## tool_label_bindings

```
dify-# \d tool_label_bindings
                       Table "public.tool_label_bindings"
   Column   |         Type          | Collation | Nullable |      Default       
------------+-----------------------+-----------+----------+--------------------
 id         | uuid                  |           | not null | uuid_generate_v4()
 tool_id    | character varying(64) |           | not null | 
 tool_type  | character varying(40) |           | not null | 
 label_name | character varying(40) |           | not null | 
Indexes:
    "tool_label_bind_pkey" PRIMARY KEY, btree (id)
    "unique_tool_label_bind" UNIQUE CONSTRAINT, btree (tool_id, label_name)
```

## tool_model_invokes

```
dify-# \d tool_model_invokes
                                   Table "public.tool_model_invokes"
          Column           |            Type             | Collation | Nullable |       Default        
---------------------------+-----------------------------+-----------+----------+----------------------
 id                        | uuid                        |           | not null | uuid_generate_v4()
 user_id                   | uuid                        |           | not null | 
 tenant_id                 | uuid                        |           | not null | 
 provider                  | character varying(40)       |           | not null | 
 tool_type                 | character varying(40)       |           | not null | 
 tool_name                 | character varying(40)       |           | not null | 
 model_parameters          | text                        |           | not null | 
 prompt_messages           | text                        |           | not null | 
 model_response            | text                        |           | not null | 
 prompt_tokens             | integer                     |           | not null | 0
 answer_tokens             | integer                     |           | not null | 0
 answer_unit_price         | numeric(10,4)               |           | not null | 
 answer_price_unit         | numeric(10,7)               |           | not null | 0.001
 provider_response_latency | double precision            |           | not null | 0
 total_price               | numeric(10,7)               |           |          | 
 currency                  | character varying(255)      |           | not null | 
 created_at                | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at                | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "tool_model_invoke_pkey" PRIMARY KEY, btree (id)
```

## tool_providers

```
dify-# \d tool_providers
                                   Table "public.tool_providers"
        Column         |            Type             | Collation | Nullable |       Default        
-----------------------+-----------------------------+-----------+----------+----------------------
 id                    | uuid                        |           | not null | uuid_generate_v4()
 tenant_id             | uuid                        |           | not null | 
 tool_name             | character varying(40)       |           | not null | 
 encrypted_credentials | text                        |           |          | 
 is_enabled            | boolean                     |           | not null | false
 created_at            | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at            | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "tool_provider_pkey" PRIMARY KEY, btree (id)
    "unique_tool_provider_tool_name" UNIQUE CONSTRAINT, btree (tenant_id, tool_name)
```

## tool_published_apps

```
dify-# \d tool_published_apps
                              Table "public.tool_published_apps"
      Column       |            Type             | Collation | Nullable |       Default        
-------------------+-----------------------------+-----------+----------+----------------------
 id                | uuid                        |           | not null | uuid_generate_v4()
 app_id            | uuid                        |           | not null | 
 user_id           | uuid                        |           | not null | 
 description       | text                        |           | not null | 
 llm_description   | text                        |           | not null | 
 query_description | text                        |           | not null | 
 query_name        | character varying(40)       |           | not null | 
 tool_name         | character varying(40)       |           | not null | 
 author            | character varying(40)       |           | not null | 
 created_at        | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at        | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "published_app_tool_pkey" PRIMARY KEY, btree (id)
    "unique_published_app_tool" UNIQUE CONSTRAINT, btree (app_id, user_id)
Foreign-key constraints:
    "tool_published_apps_app_id_fkey" FOREIGN KEY (app_id) REFERENCES apps(id)
```

## tool_workflow_providers

```
dify-# \d tool_workflow_providers
                                Table "public.tool_workflow_providers"
         Column          |            Type             | Collation | Nullable |        Default        
-------------------------+-----------------------------+-----------+----------+-----------------------
 id                      | uuid                        |           | not null | uuid_generate_v4()
 name                    | character varying(40)       |           | not null | 
 icon                    | character varying(255)      |           | not null | 
 app_id                  | uuid                        |           | not null | 
 user_id                 | uuid                        |           | not null | 
 tenant_id               | uuid                        |           | not null | 
 description             | text                        |           | not null | 
 parameter_configuration | text                        |           | not null | '[]'::text
 created_at              | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at              | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 privacy_policy          | character varying(255)      |           |          | ''::character varying
 version                 | character varying(255)      |           | not null | ''::character varying
 label                   | character varying(255)      |           | not null | ''::character varying
Indexes:
    "tool_workflow_provider_pkey" PRIMARY KEY, btree (id)
    "unique_workflow_tool_provider" UNIQUE CONSTRAINT, btree (name, tenant_id)
    "unique_workflow_tool_provider_app_id" UNIQUE CONSTRAINT, btree (tenant_id, app_id)
```

## trace_app_config

```
dify-# \d trace_app_config
                              Table "public.trace_app_config"
      Column      |            Type             | Collation | Nullable |      Default       
------------------+-----------------------------+-----------+----------+--------------------
 id               | uuid                        |           | not null | uuid_generate_v4()
 app_id           | uuid                        |           | not null | 
 tracing_provider | character varying(255)      |           |          | 
 tracing_config   | json                        |           |          | 
 created_at       | timestamp without time zone |           | not null | now()
 updated_at       | timestamp without time zone |           | not null | now()
 is_active        | boolean                     |           | not null | true
Indexes:
    "trace_app_config_pkey" PRIMARY KEY, btree (id)
    "trace_app_config_app_id_idx" btree (app_id)
```

## upload_files

```
dify-# \d upload_files
                                     Table "public.upload_files"
     Column      |            Type             | Collation | Nullable |           Default            
-----------------+-----------------------------+-----------+----------+------------------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 tenant_id       | uuid                        |           | not null | 
 storage_type    | character varying(255)      |           | not null | 
 key             | character varying(255)      |           | not null | 
 name            | character varying(255)      |           | not null | 
 size            | integer                     |           | not null | 
 extension       | character varying(255)      |           | not null | 
 mime_type       | character varying(255)      |           |          | 
 created_by      | uuid                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 used            | boolean                     |           | not null | false
 used_by         | uuid                        |           |          | 
 used_at         | timestamp without time zone |           |          | 
 hash            | character varying(255)      |           |          | 
 created_by_role | character varying(255)      |           | not null | 'account'::character varying
Indexes:
    "upload_file_pkey" PRIMARY KEY, btree (id)
    "upload_file_tenant_idx" btree (tenant_id)
```

## workflow_app_logs

```
dify-# \d workflow_app_logs
                              Table "public.workflow_app_logs"
     Column      |            Type             | Collation | Nullable |       Default        
-----------------+-----------------------------+-----------+----------+----------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 tenant_id       | uuid                        |           | not null | 
 app_id          | uuid                        |           | not null | 
 workflow_id     | uuid                        |           | not null | 
 workflow_run_id | uuid                        |           | not null | 
 created_from    | character varying(255)      |           | not null | 
 created_by_role | character varying(255)      |           | not null | 
 created_by      | uuid                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
Indexes:
    "workflow_app_log_pkey" PRIMARY KEY, btree (id)
    "workflow_app_log_app_idx" btree (tenant_id, app_id)
```

## workflow_conversation_variables

```
dify-# \d workflow_conversation_variables
                       Table "public.workflow_conversation_variables"
     Column      |            Type             | Collation | Nullable |       Default        
-----------------+-----------------------------+-----------+----------+----------------------
 id              | uuid                        |           | not null | 
 conversation_id | uuid                        |           | not null | 
 app_id          | uuid                        |           | not null | 
 data            | text                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP
Indexes:
    "workflow__conversation_variables_pkey" PRIMARY KEY, btree (id, conversation_id)
    "workflow__conversation_variables_app_id_idx" btree (app_id)
    "workflow__conversation_variables_created_at_idx" btree (created_at)
```

## workflow_node_executions

```
dify-# \d workflow_node_executions
                             Table "public.workflow_node_executions"
       Column        |            Type             | Collation | Nullable |       Default        
---------------------+-----------------------------+-----------+----------+----------------------
 id                  | uuid                        |           | not null | uuid_generate_v4()
 tenant_id           | uuid                        |           | not null | 
 app_id              | uuid                        |           | not null | 
 workflow_id         | uuid                        |           | not null | 
 triggered_from      | character varying(255)      |           | not null | 
 workflow_run_id     | uuid                        |           |          | 
 index               | integer                     |           | not null | 
 predecessor_node_id | character varying(255)      |           |          | 
 node_id             | character varying(255)      |           | not null | 
 node_type           | character varying(255)      |           | not null | 
 title               | character varying(255)      |           | not null | 
 inputs              | text                        |           |          | 
 process_data        | text                        |           |          | 
 outputs             | text                        |           |          | 
 status              | character varying(255)      |           | not null | 
 error               | text                        |           |          | 
 elapsed_time        | double precision            |           | not null | 0
 execution_metadata  | text                        |           |          | 
 created_at          | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 created_by_role     | character varying(255)      |           | not null | 
 created_by          | uuid                        |           | not null | 
 finished_at         | timestamp without time zone |           |          | 
Indexes:
    "workflow_node_execution_pkey" PRIMARY KEY, btree (id)
    "workflow_node_execution_node_run_idx" btree (tenant_id, app_id, workflow_id, triggered_from, node_id)
    "workflow_node_execution_workflow_run_idx" btree (tenant_id, app_id, workflow_id, triggered_from, workflow_run_id)
```

## workflow_runs

```
dify-# \d workflow_runs
                                Table "public.workflow_runs"
     Column      |            Type             | Collation | Nullable |       Default        
-----------------+-----------------------------+-----------+----------+----------------------
 id              | uuid                        |           | not null | uuid_generate_v4()
 tenant_id       | uuid                        |           | not null | 
 app_id          | uuid                        |           | not null | 
 sequence_number | integer                     |           | not null | 
 workflow_id     | uuid                        |           | not null | 
 type            | character varying(255)      |           | not null | 
 triggered_from  | character varying(255)      |           | not null | 
 version         | character varying(255)      |           | not null | 
 graph           | text                        |           |          | 
 inputs          | text                        |           |          | 
 status          | character varying(255)      |           | not null | 
 outputs         | text                        |           |          | 
 error           | text                        |           |          | 
 elapsed_time    | double precision            |           | not null | 0
 total_tokens    | integer                     |           | not null | 0
 total_steps     | integer                     |           |          | 0
 created_by_role | character varying(255)      |           | not null | 
 created_by      | uuid                        |           | not null | 
 created_at      | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 finished_at     | timestamp without time zone |           |          | 
Indexes:
    "workflow_run_pkey" PRIMARY KEY, btree (id)
    "workflow_run_tenant_app_sequence_idx" btree (tenant_id, app_id, sequence_number)
    "workflow_run_triggerd_from_idx" btree (tenant_id, app_id, triggered_from)
```

## workflows

```
dify-# \d workflows
                                      Table "public.workflows"
         Column         |            Type             | Collation | Nullable |       Default        
------------------------+-----------------------------+-----------+----------+----------------------
 id                     | uuid                        |           | not null | uuid_generate_v4()
 tenant_id              | uuid                        |           | not null | 
 app_id                 | uuid                        |           | not null | 
 type                   | character varying(255)      |           | not null | 
 version                | character varying(255)      |           | not null | 
 graph                  | text                        |           |          | 
 features               | text                        |           |          | 
 created_by             | uuid                        |           | not null | 
 created_at             | timestamp without time zone |           | not null | CURRENT_TIMESTAMP(0)
 updated_by             | uuid                        |           |          | 
 updated_at             | timestamp without time zone |           |          | 
 environment_variables  | text                        |           | not null | '{}'::text
 conversation_variables | text                        |           | not null | '{}'::text
Indexes:
    "workflow_pkey" PRIMARY KEY, btree (id)
    "workflow_version_idx" btree (tenant_id, app_id, version)
```
