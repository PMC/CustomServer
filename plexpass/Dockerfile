FROM linuxserver/plex:latest 
LABEL org.freenas.interactive="false" 		\
      org.freenas.version="Latest (Auto Update)"		\
      org.freenas.upgradeable="true"		\
      org.freenas.expose-ports-at-host="true"	\
      org.freenas.autostart="true"		\
      org.freenas.capabilities-add="NET_BROADCAST" \
      org.freenas.web-ui-protocol="https"	\
      org.freenas.web-ui-port=32400		\
      org.freenas.web-ui-path="web"		\
      org.freenas.port-mappings="32400:32400/tcp,32469:32469/tcp,1900:5353/udp"			\
      org.freenas.volumes="[					\
          {							\
              \"name\": \"/config\",				\
              \"descr\": \"Config storage space\"		\
          },							\
          {							\
              \"name\": \"/transcode\",				\
              \"descr\": \"Video transcode directory\"		\
          },							\
          {							\
              \"name\": \"/data\",				\
              \"descr\": \"Media volume\"			\
          }							\
      ]"							\
      org.freenas.settings="[ 					\
          {							\
              \"env\": \"TZ\",					\
              \"descr\": \"Plex container Timezone\",		\
              \"optional\": true				\
          },							\
          {							\
              \"env\": \"PUID\",				\
              \"descr\": \"Plex User ID\",			\
              \"optional\": true				\
          },							\
          {							\
              \"env\": \"PGID\",				\
              \"descr\": \"Plex Group ID\",			\
              \"optional\": true				\
          },							\
          {							\
              \"env\": \"VERSION\",				\
              \"descr\": \"Set whether to update plex or not (latest)\",			\
              \"optional\": true				\
          } \
      ]"
