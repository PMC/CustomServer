FROM lsiobase/xenial
MAINTAINER pmc, original from Linuxserver

# global environment settings
ENV DEBIAN_FRONTEND="noninteractive" \
PLEX_DOWNLOAD="https://downloads.plex.tv/plex-media-server" \
PLEX_INSTALL="https://plex.tv/downloads/latest/1?channel=8&build=linux-ubuntu-x86_64&distro=ubuntu" \
PLEX_MEDIA_SERVER_APPLICATION_SUPPORT_DIR="/config/Library/Application Support" \
PLEX_MEDIA_SERVER_HOME="/usr/lib/plexmediaserver" \
PLEX_MEDIA_SERVER_INFO_DEVICE=docker \
PLEX_MEDIA_SERVER_MAX_PLUGIN_PROCS="6" \
PLEX_MEDIA_SERVER_USER=abc

# install packages
RUN \
 apt-get update && \
 apt-get install -y \
	avahi-daemon \
	dbus \
	wget && \

# install plex
 curl -o \
	/tmp/plexmediaserver.deb -L \
	"${PLEX_INSTALL}" && \
 dpkg -i /tmp/plexmediaserver.deb && \

# change abc home folder to fix plex hanging at runtime with usermod
 usermod -d /app abc && \

# cleanup
 apt-get clean && \
 rm -rf \
	/etc/default/plexmediaserver \
	/tmp/* \
	/var/lib/apt/lists/* \
	/var/tmp/*

# add local files
COPY root/ /

# ports and volumes
EXPOSE 32400 32400/udp 32469 32469/udp 1900/udp 32410/udp 32412/udp 32413/udp 32414/udp
VOLUME /config /transcode
# FreeNAS stuff
LABEL org.freenas.interactive="false" 		\
      org.freenas.version="Latest (Auto Update)"		\
      org.freenas.upgradeable="true"		\
      org.freenas.expose-ports-at-host="true"	\
      org.freenas.autostart="true"		\
      org.freenas.capabilities-add="NET_BROADCAST" \
      org.freenas.web-ui-protocol="https"	\
      org.freenas.web-ui-port=32400		\
      org.freenas.web-ui-path="web"		\
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
