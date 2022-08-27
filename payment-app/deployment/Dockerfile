FROM node:14.15.3-alpine

# setup WORK_DIR then copy files for installation
ARG WORK_DIR=/app
RUN mkdir -p ${WORK_DIR}
COPY . ${WORK_DIR}/
WORKDIR ${WORK_DIR}

# Pass in build-time arg via docker-composee
ARG SAMPLE_AUTH_TOKEN

RUN apk update && apk upgrade && apk add --no-cache bash git
RUN npm install

EXPOSE 3400
ENTRYPOINT [ "npm", "start" ]
