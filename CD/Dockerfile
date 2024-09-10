ARG DOCKER_IMAGE_CI
ARG DOCKER_IMAGE_CD
ARG DOCKER_IMAGE_BASE

# ################################### IMAGE CONSOLIDATION################################

FROM ${DOCKER_IMAGE_BASE} AS builder
WORKDIR /opt/app-root
COPY package.json .
RUN npm install --no-fund
COPY . .
RUN npm run build
RUN ls -lrt /opt/app-root/dist

# ################################### IMAGE CONSOLIDATION################################

FROM ${DOCKER_IMAGE_BASE} AS nodeprod
WORKDIR /opt/app-root
COPY package.json .
RUN npm install --no-optional --no-fund --omit=dev
COPY . .
COPY --from=builder /opt/app-root/dist ./dist
RUN ls -lrt /opt/app-root/dist
EXPOSE 8080
CMD ["npm", "start"]


