# matrix

![Version: 4.0.5](https://img.shields.io/badge/Version-4.0.5-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: v1.88.0](https://img.shields.io/badge/AppVersion-v1.88.0-informational?style=flat-square)

A Helm chart to deploy a Matrix homeserver stack into Kubernetes

**Homepage:** <https://github.com/jessebot/matrix-chart>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Arkaniad | <rhea@isomemetric.com> | <https://github.com/Arkaniad/> |
| jessebot | <jessebot@linux.com> | <https://github.com/jessebot/> |

## Source Code

* <https://github.com/jessebot/matrix-chart>

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://jessebot.github.io/coturn-chart | coturn | 3.0.4 |
| oci://registry-1.docker.io/bitnamicharts | postgresql | 12.6.9 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| bridges.affinity | bool | `false` | Recommended to leave this disabled to allow bridges to be scheduled on separate nodes. Set this to true to reduce latency between the homeserver and bridges, or if your cloud provider does not allow the ReadWriteMany access mode (see below) |
| bridges.discord.auth.botToken | string | `""` | Discord bot token for authentication |
| bridges.discord.auth.clientId | string | `""` | Discord bot clientID for authentication |
| bridges.discord.channelName | string | `"[Discord] :guild :name"` |  |
| bridges.discord.data.capacity | string | `"512Mi"` |  |
| bridges.discord.data.storageClass | string | `""` |  |
| bridges.discord.defaultVisibility | string | `"public"` |  |
| bridges.discord.enabled | bool | `false` | Set to true to enable the Discord bridge |
| bridges.discord.image.pullPolicy | string | `"Always"` |  |
| bridges.discord.image.repository | string | `"halfshot/matrix-appservice-discord"` |  |
| bridges.discord.image.tag | string | `"latest"` |  |
| bridges.discord.joinLeaveEvents | bool | `true` |  |
| bridges.discord.presence | bool | `true` |  |
| bridges.discord.readReceipt | bool | `true` |  |
| bridges.discord.replicaCount | int | `1` |  |
| bridges.discord.resources | object | `{}` |  |
| bridges.discord.selfService | bool | `false` |  |
| bridges.discord.service.port | int | `9005` |  |
| bridges.discord.service.type | string | `"ClusterIP"` |  |
| bridges.discord.typingNotifications | bool | `true` |  |
| bridges.discord.users.nickname | string | `":nick"` |  |
| bridges.discord.users.username | string | `":username#:tag"` |  |
| bridges.irc.data.capacity | string | `"1Mi"` | Size of the data PVC to allocate |
| bridges.irc.database | string | `"matrix_irc"` | Postgres database to store IRC bridge data in, this db will be created if postgresql.enabled: true, otherwise you must create it manually |
| bridges.irc.databaseSslVerify | bool | `true` |  |
| bridges.irc.enabled | bool | `false` | Set to true to enable the IRC bridge |
| bridges.irc.image.pullPolicy | string | `"IfNotPresent"` |  |
| bridges.irc.image.repository | string | `"matrixdotorg/matrix-appservice-irc"` |  |
| bridges.irc.image.tag | string | `"release-1.0.0"` |  |
| bridges.irc.presence | bool | `false` | Whether to enable presence (online/offline indicators). If presence is disabled for the homeserver (above), it should be disabled here too |
| bridges.irc.replicaCount | int | `1` |  |
| bridges.irc.resources | object | `{}` |  |
| bridges.irc.servers."chat.freenode.net".name | string | `"Freenode"` | A human-readable short name. |
| bridges.irc.servers."chat.freenode.net".port | int | `6697` | The port to connect to. Optional. |
| bridges.irc.servers."chat.freenode.net".ssl | bool | `true` | Whether to use SSL or not. Default: false. |
| bridges.irc.service.port | int | `9006` |  |
| bridges.irc.service.type | string | `"ClusterIP"` |  |
| bridges.volume.accessMode | string | `"ReadWriteMany"` | Access mode of the shared volume. ReadWriteMany is recommended to allow bridges to be scheduled on separate nodes. Some cloud providers may not allow the ReadWriteMany access mode. In that case, change this to ReadWriteOnce AND set bridges.affinity (above) to true |
| bridges.volume.capacity | string | `"1Mi"` | Capacity of the shared volume for storing bridge/appservice registration files. Note: 1Mi should be enough but some cloud providers may set a minimum PVC size of 1Gi, adjust as necessary |
| bridges.volume.existingClaim | string | `""` | name of an existing persistent volume claim to use for bridges |
| bridges.volume.storageClass | string | `""` | Storage class (optional) |
| bridges.whatsapp.bot.avatar | string | `"mxc://maunium.net/NeXNQarUbrlYBiPCpprYsRqr"` | avatar of the WhatsApp bridge bot |
| bridges.whatsapp.bot.displayName | string | `"WhatsApp bridge bot"` | display name of the WhatsApp bridge bot |
| bridges.whatsapp.bot.username | string | `"whatsappbot"` | Username of the WhatsApp bridge bot |
| bridges.whatsapp.callNotices | bool | `true` | Send notifications for incoming calls |
| bridges.whatsapp.communityName | string | `"whatsapp_{{.Localpart}}={{.Server}}"` | Display name for communities. A community will be automatically generated for each user using the bridge, and can be used to group WhatsApp chats together. Evaluated as a template, with variables: {{.Localpart}} - MXID localpart {{.Server}}    - MXID server part of the user. |
| bridges.whatsapp.connection.maxAttempts | int | `3` | Maximum number of connection attempts before failing |
| bridges.whatsapp.connection.qrRegenCount | int | `2` | Number of QR codes to store, which multiplies the connection timeout |
| bridges.whatsapp.connection.reportRetry | bool | `true` | Whether or not to notify the user when attempting to reconnect. Set to false to only report when maxAttempts has been reached |
| bridges.whatsapp.connection.retryDelay | int | `-1` | Retry delay. Negative numbers are exponential backoff: -connection_retry_delay + 1 + 2^attempts |
| bridges.whatsapp.connection.timeout | int | `20` | WhatsApp server connection timeout (seconds) |
| bridges.whatsapp.data.capacity | string | `"512Mi"` | Size of the PVC to allocate for the SQLite database |
| bridges.whatsapp.data.storageClass | string | `""` | Storage class (optional) |
| bridges.whatsapp.enabled | bool | `false` | Set to true to enable the WhatsApp bridge |
| bridges.whatsapp.image.pullPolicy | string | `"Always"` |  |
| bridges.whatsapp.image.repository | string | `"dock.mau.dev/tulir/mautrix-whatsapp"` |  |
| bridges.whatsapp.image.tag | string | `"latest"` |  |
| bridges.whatsapp.permissions | object | `{"*":"relaybot"}` | Permissions for using the bridge. Permitted values: relaybot - Talk through the relaybot (if enabled), no access otherwise     user - Access to use the bridge to chat with a WhatsApp account.    admin - User level and some additional administration tools Permitted keys:        * - All Matrix users   domain - All users on that homeserver     mxid - Specific user |
| bridges.whatsapp.relaybot.enabled | bool | `false` | Set to true to enable the relaybot and management room |
| bridges.whatsapp.relaybot.invites | list | `[]` |  |
| bridges.whatsapp.relaybot.management | string | `"!foo:example.com"` | Management room for the relay bot where status notifs are posted |
| bridges.whatsapp.replicaCount | int | `1` |  |
| bridges.whatsapp.resources | object | `{}` |  |
| bridges.whatsapp.service.port | int | `29318` |  |
| bridges.whatsapp.service.type | string | `"ClusterIP"` |  |
| bridges.whatsapp.users.displayName | string | `"{{if .Notify}}{{.Notify}}{{else}}{{.Jid}}{{end}} (WA)"` | Display name for WhatsApp users Evaluated as a template, with variables: {{.Notify}} - nickname set by the WhatsApp user {{.Jid}}    - phone number (international format) following vars are available, but cause issue on multi-user instances: {{.Name}}   - display name from contact list {{.Short}}  - short display name from contact list |
| bridges.whatsapp.users.username | string | `"whatsapp_{{.}}"` | Username for WhatsApp users. Evaluated as a template where {{.}} is replaced with the phone number of the WhatsApp user |
| coturn.allowGuests | bool | `true` | Whether to allow guests to use the TURN server |
| coturn.certificate.enabled | bool | `false` | set to true to generate a TLS certificate for encrypted comms |
| coturn.certificate.host | string | `"turn.example.com"` | hostname for TLS cert |
| coturn.certificate.issuerName | string | `"letsencrypt-staging"` | cert-manager cert Issuer or ClusterIssuer to use |
| coturn.enabled | bool | `true` | Set to false to disable the included deployment of Coturn |
| coturn.existingSecret | string | `""` | Optional: name of an existingSecret with key for sharedSecret |
| coturn.ports | object | `{"from":3478,"to":3478}` | UDP port range for TURN connections |
| coturn.secretKey | string | `"coturnSharedSecret"` | key in existing secret with sharedSecret value. Required if coturn.enabled=true and existingSecret not "" |
| coturn.service.type | string | `"ClusterIP"` |  |
| coturn.sharedSecret | string | `""` | shared secert for comms b/w Synapse/Coturn. autogenerated if not provided |
| coturn.uris | list | `[]` | URIs of the Coturn servers. If deploying Coturn with this chart, include the public IPs of each node in your cluster (or a DNS round-robin hostname) You can also include an external Coturn instance if you'd prefer |
| element.branding.authFooterLinks | list | `[]` | Array of links to show at the bottom of the login screen |
| element.branding.authHeaderLogoUrl | string | `""` | Logo shown at top of login screen |
| element.branding.brand | string | `"Element"` | brand shown in email notifications |
| element.branding.welcomeBackgroundUrl | string | `""` | Background of login splash screen |
| element.enabled | bool | `true` | Set to false to disable a deployment of Element. Users will still be able to connect via any other instances of Element e.g. https://app.element.io, Element Desktop, or any other Matrix clients |
| element.image.pullPolicy | string | `"IfNotPresent"` | pullPolicy to use for element image, set to Always if using latest tag |
| element.image.repository | string | `"vectorim/element-web"` | registry and repository to use for element docker image |
| element.image.tag | string | `"v1.11.36"` | tag to use for element docker image |
| element.ingress.annotations."cert-manager.io/cluster-issuer" | string | `"letsencrypt-staging"` | required for TLS certs issued by cert-manager |
| element.ingress.annotations."nginx.ingress.kubernetes.io/configuration-snippet" | string | `"proxy_intercept_errors off;\n"` |  |
| element.ingress.enabled | bool | `true` | enable ingress for element |
| element.ingress.host | string | `"element.chart-example.local"` | the hostname to use for element |
| element.ingress.tls.enabled | bool | `true` |  |
| element.integrations.api | string | `"https://scalar.vector.im/api"` | API for the integration server |
| element.integrations.enabled | bool | `true` | enables the Integrations menu, including:    widgets, bots, and other plugins to Element |
| element.integrations.ui | string | `"https://scalar.vector.im/"` | UI to load when a user selects the Integrations button at the top-right    of a room |
| element.integrations.widgets | list | `["https://scalar.vector.im/_matrix/integrations/v1","https://scalar.vector.im/api","https://scalar-staging.vector.im/_matrix/integrations/v1","https://scalar-staging.vector.im/api","https://scalar-staging.element.im/scalar/api"]` | Array of API paths providing widgets |
| element.labels | object | `{"component":"element"}` | Element specific labels |
| element.labs | list | `["feature_new_spinner","feature_pinning","feature_custom_status","feature_custom_tags","feature_state_counters","feature_many_integration_managers","feature_mjolnir","feature_dm_verification","feature_bridge_state","feature_presence_in_room_list","feature_custom_themes"]` | Experimental features in Element, see: https://github.com/vector-im/element-web/blob/develop/docs/labs.md |
| element.permalinkPrefix | string | `"https://matrix.to"` | Prefix before permalinks generated when users share links to rooms, users, or messages. If running an unfederated Synapse, set the below to the URL of your Element instance. |
| element.probes.liveness | object | `{}` |  |
| element.probes.readiness | object | `{}` |  |
| element.probes.startup | object | `{}` |  |
| element.replicaCount | int | `1` |  |
| element.resources | object | `{}` |  |
| element.roomDirectoryServers | list | `["matrix.org"]` | Servers to show in the Explore menu (the current server is always shown) |
| element.service.port | int | `80` |  |
| element.service.type | string | `"ClusterIP"` |  |
| element.welcomeUserId | string | `""` | Set to the user ID (@username:domain.tld) of a bot to invite all new users to a DM with the bot upon registration |
| fullnameOverride | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| mail.elementUrl | string | `""` | Optional: Element instance URL. If ingress is enabled, this is unnecessary, else if this is empty, emails will contain a link to https://app.element.io |
| mail.enabled | bool | `false` | disabled all email notifications by default. NOTE: If enabled, either enable the Exim relay or configure an external mail server below |
| mail.external.host | string | `""` | External mail server hostname |
| mail.external.password | string | `""` | External mail server password |
| mail.external.port | int | `25` | External mail server port |
| mail.external.requireTransportSecurity | bool | `true` |  |
| mail.external.username | string | `""` | External mail server username |
| mail.from | string | `"Matrix <matrix@example.com>"` | Name and email address for outgoing mail |
| mail.relay.enabled | bool | `true` | whether to enable exim relay or not |
| mail.relay.image.pullPolicy | string | `"IfNotPresent"` |  |
| mail.relay.image.repository | string | `"devture/exim-relay"` |  |
| mail.relay.image.tag | string | `"4.95-r0"` |  |
| mail.relay.labels.component | string | `"mail"` |  |
| mail.relay.probes.liveness | object | `{}` |  |
| mail.relay.probes.readiness | object | `{}` |  |
| mail.relay.probes.startup | object | `{}` |  |
| mail.relay.replicaCount | int | `1` |  |
| mail.relay.resources | object | `{}` |  |
| mail.relay.service.port | int | `25` |  |
| mail.relay.service.type | string | `"ClusterIP"` |  |
| matrix.adminEmail | string | `"admin@example.com"` | Email address of the administrator |
| matrix.blockNonAdminInvites | bool | `false` | Set to true to block non-admins from inviting users to any rooms |
| matrix.disabled | bool | `false` | Set to true to globally block access to the homeserver |
| matrix.disabledMessage | string | `""` | Human readable reason for why the homeserver is blocked |
| matrix.encryptByDefault | string | `"invite"` |  |
| matrix.federation.allowPublicRooms | bool | `true` | Allow members of other homeservers to fetch *public* rooms |
| matrix.federation.blacklist | list | `["127.0.0.0/8","10.0.0.0/8","172.16.0.0/12","192.168.0.0/16","100.64.0.0/10","169.254.0.0/16","::1/128","fe80::/64","fc00::/7"]` | IP addresses to blacklist federation requests to |
| matrix.federation.enabled | bool | `true` | Set to false to disable federation and run an isolated homeserver |
| matrix.federation.ingress.annotations."cert-manager.io/cluster-issuer" | string | `"letsencrypt-staging"` | required for TLS certs issued by cert-manager |
| matrix.federation.ingress.annotations."nginx.ingress.kubernetes.io/configuration-snippet" | string | `"proxy_intercept_errors off;\n"` | required for the Nginx ingress provider. You can remove it if you use a different ingress provider |
| matrix.federation.ingress.enabled | bool | `true` |  |
| matrix.federation.ingress.host | string | `"matrix-fed.chart-example.local"` |  |
| matrix.federation.ingress.tls.enabled | bool | `true` |  |
| matrix.federation.whitelist | list | `[]` | Allow list of domains to federate with (comment for all domains    except blacklisted) |
| matrix.homeserverExtra | object | `{}` | Contents will be appended to the end of the default configuration |
| matrix.homeserverOverride | object | `{}` | Replace homeserver.yaml will be replaced with these contents |
| matrix.logging.rootLogLevel | string | `"WARNING"` | Root log level is the default log level for log outputs that don't have more specific settings. |
| matrix.logging.sqlLogLevel | string | `"WARNING"` | beware: increasing this to DEBUG will make synapse log sensitive information such as access tokens. |
| matrix.logging.synapseLogLevel | string | `"WARNING"` | The log level for the synapse server |
| matrix.presence | bool | `true` | Set to false to disable presence (online/offline indicators) |
| matrix.registration.allowGuests | bool | `false` | Allow users to join rooms as a guest |
| matrix.registration.autoJoinRooms | list | `[]` | Rooms to automatically join all new users to |
| matrix.registration.enabled | bool | `false` | Allow new users to register an account |
| matrix.registration.requiresToken | bool | `false` | Whether to allow token based registration |
| matrix.retentionPeriod | string | `"7d"` | How long to keep redacted events in unredacted form in the database |
| matrix.search | bool | `true` | Set to false to disable message searching |
| matrix.security.surpressKeyServerWarning | bool | `true` |  |
| matrix.serverName | string | `"example.com"` | Domain name of the server: This is not necessarily the host name where the service is reachable. In fact, you may want to omit any subdomains from this value as the server name set here will be the name of your homeserver in the fediverse, & will be the domain name at the end of every username |
| matrix.telemetry | bool | `false` | Enable anonymous telemetry to matrix.org |
| matrix.uploads | object | `{"maxPixels":"32M","maxSize":"10M"}` | Settings related to image and multimedia uploads |
| matrix.uploads.maxPixels | string | `"32M"` | Max image size in pixels |
| matrix.uploads.maxSize | string | `"10M"` | Max upload size in bytes |
| matrix.urlPreviews.enabled | bool | `false` | Enable URL previews. WARN: Make sure to review default rules below to ensure that users cannot crawl sensitive internal endpoints on yr cluster |
| matrix.urlPreviews.rules.ip.blacklist[0] | string | `"127.0.0.0/8"` |  |
| matrix.urlPreviews.rules.ip.blacklist[1] | string | `"10.0.0.0/8"` |  |
| matrix.urlPreviews.rules.ip.blacklist[2] | string | `"172.16.0.0/12"` |  |
| matrix.urlPreviews.rules.ip.blacklist[3] | string | `"192.168.0.0/16"` |  |
| matrix.urlPreviews.rules.ip.blacklist[4] | string | `"100.64.0.0/10"` |  |
| matrix.urlPreviews.rules.ip.blacklist[5] | string | `"169.254.0.0/16"` |  |
| matrix.urlPreviews.rules.ip.blacklist[6] | string | `"::1/128"` |  |
| matrix.urlPreviews.rules.ip.blacklist[7] | string | `"fe80::/64"` |  |
| matrix.urlPreviews.rules.ip.blacklist[8] | string | `"fc00::/7"` |  |
| matrix.urlPreviews.rules.ip.whitelist | list | `[]` |  |
| matrix.urlPreviews.rules.maxSize | string | `"10M"` | Max size of a crawlable page. Keep this low to prevent a DOS vector |
| matrix.urlPreviews.rules.url | object | `{}` | Whitelist and blacklist based on URL pattern matching |
| nameOverride | string | `""` |  |
| networkPolicies.enabled | bool | `true` | whether to enable kubernetes network policies or not |
| postgresql.enabled | bool | `true` | Whether to deploy the stable/postgresql chart with this chart. If disabled, make sure PostgreSQL is available at the hostname below and credentials are configured under postgresql.global.postgresql.auth |
| postgresql.global.postgresql.auth.existingSecret | string | `""` | Name of existing secret to use for PostgreSQL credentials |
| postgresql.global.postgresql.auth.hostname | string | `""` | hostname of db server. Can be left blank if using postgres subchart |
| postgresql.global.postgresql.auth.password | string | `"changeme"` | password of matrix postgres user - ignored using exsitingSecret |
| postgresql.global.postgresql.auth.port | int | `5432` | which port to use to connect to your database server |
| postgresql.global.postgresql.auth.secretKeys.adminPasswordKey | string | `"postgresPassword"` | key in existingSecret with the admin postgresql password |
| postgresql.global.postgresql.auth.secretKeys.database | string | `"database"` | key in existingSecret with name of the database |
| postgresql.global.postgresql.auth.secretKeys.databaseHostname | string | `"hostname"` | key in existingSecret with hostname of the database |
| postgresql.global.postgresql.auth.secretKeys.databaseUsername | string | `"username"` | key in existingSecret with username for matrix to connect to db |
| postgresql.global.postgresql.auth.secretKeys.userPasswordKey | string | `"password"` | key in existingSecret with password for matrix to connect to db |
| postgresql.global.postgresql.auth.username | string | `"matrix"` | username of matrix postgres user |
| postgresql.primary.initdb | object | `{"scriptsConfigMap":"{{ .Release.Name }}-postgresql-initdb"}` | run the scripts in templates/postgresql/initdb-configmap.yaml If using an external Postgres server, make sure to configure the database ref: https://github.com/matrix-org/synapse/blob/master/docs/postgres.md |
| postgresql.primary.persistence | object | `{"enabled":false,"size":"8Gi"}` | persistent volume claim configuration for postgresql to persist data |
| postgresql.primary.persistence.enabled | bool | `false` | Enable PostgreSQL Primary data persistence using PVC |
| postgresql.primary.persistence.size | string | `"8Gi"` | size of postgresql volume claim |
| postgresql.primary.podSecurityContext.enabled | bool | `true` |  |
| postgresql.primary.podSecurityContext.fsGroup | int | `1000` |  |
| postgresql.primary.podSecurityContext.runAsUser | int | `1000` |  |
| postgresql.volumePermissions.enabled | bool | `true` | Enable init container that changes the owner and group of the PVC |
| synapse.extraVolumeMounts | list | `[]` |  |
| synapse.extraVolumes | list | `[]` |  |
| synapse.image.pullPolicy | string | `"IfNotPresent"` | pullPolicy for synapse image, Use Always if using image.tag: latest |
| synapse.image.repository | string | `"matrixdotorg/synapse"` | image registry and repository to use for synapse |
| synapse.image.tag | string | `""` | tag of synapse docker image to use. change this to latest to grab the    cutting-edge release of synapse |
| synapse.ingress.annotations."cert-manager.io/cluster-issuer" | string | `"letsencrypt-staging"` | required for TLS certs issued by cert-manager |
| synapse.ingress.annotations."nginx.ingress.kubernetes.io/configuration-snippet" | string | `"proxy_intercept_errors off;\n"` | This annotation is required for the Nginx ingress provider. You can remove it if you use a different ingress provider |
| synapse.ingress.enabled | bool | `true` |  |
| synapse.ingress.host | string | `"matrix.chart-example.local"` |  |
| synapse.ingress.tls.enabled | bool | `true` |  |
| synapse.labels | object | `{"component":"synapse"}` | Labels to be appended to all Synapse resources |
| synapse.metrics.annotations | bool | `true` |  |
| synapse.metrics.enabled | bool | `true` | Whether Synapse should capture metrics on an additional endpoint |
| synapse.metrics.port | int | `9092` | Port to listen on for metrics scraping |
| synapse.probes.liveness.periodSeconds | int | `10` | liveness probe seconds trying again |
| synapse.probes.liveness.timeoutSeconds | int | `5` | liveness probe seconds before timing out |
| synapse.probes.readiness.periodSeconds | int | `10` | readiness probe seconds trying again |
| synapse.probes.readiness.timeoutSeconds | int | `5` | readiness probe seconds before timing out |
| synapse.probes.startup.failureThreshold | int | `6` | startup probe times to try and fail before giving up |
| synapse.probes.startup.periodSeconds | int | `5` | startup probe seconds trying again |
| synapse.probes.startup.timeoutSeconds | int | `5` | startup probe seconds before timing out |
| synapse.replicaCount | int | `1` |  |
| synapse.resources | object | `{}` |  |
| synapse.securityContext.env | bool | `false` | Enable if your k8s environment allows containers to chuser/setuid https://github.com/matrix-org/synapse/blob/96cf81e312407f0caba1b45ba9899906b1dcc098/docker/start.py#L196 |
| synapse.securityContext.fsGroup | int | `1000` |  |
| synapse.securityContext.runAsGroup | int | `1000` | group to run the synapse container as |
| synapse.securityContext.runAsNonRoot | bool | `true` |  |
| synapse.securityContext.runAsUser | int | `1000` | user to run the synapse container as |
| synapse.service.federation.port | int | `80` |  |
| synapse.service.federation.type | string | `"ClusterIP"` |  |
| synapse.service.port | int | `80` | service port for synapse |
| synapse.service.type | string | `"ClusterIP"` | service type for synpase |
| volumes.media.capacity | string | `"10Gi"` | Capacity of the media PVC - ignored if using exsitingClaim |
| volumes.media.existingClaim | string | `""` | name of an existing PVC to use for uploaded attachments and multimedia |
| volumes.media.storageClass | string | `""` | Storage class of the media PVC - ignored if using exsitingClaim |
| volumes.signingKey.capacity | string | `"1Mi"` | Capacity of the signing key PVC. Note: 1Mi is more than enough, but some cloud providers set a min PVC size of 1Mi or 1Gi, adjust as necessary |
| volumes.signingKey.existingClaim | string | `""` | name of an existing persistent volume claim to use for signing key |
| volumes.signingKey.storageClass | string | `""` | Storage class (optional) |
| volumes.synapseConfig.capacity | string | `"1Mi"` | Capacity of the signing key PVC. Note: 1Mi is more than enough, but some cloud providers set a min PVC size of 1Mi or 1Gi, adjust as necessary |
| volumes.synapseConfig.existingClaim | string | `""` | name of an existing persistent volume claim for synapse config file |
| volumes.synapseConfig.storageClass | string | `""` | Storage class (optional) |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.11.0](https://github.com/norwoodj/helm-docs/releases/v1.11.0)
