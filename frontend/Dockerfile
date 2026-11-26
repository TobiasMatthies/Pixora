FROM node:26.13.0-bookworm-slim AS builder
COPY --from=ghcr.io/pnpm/pnpm:12 /opt/pnpm /opt/pnpm
RUN for bin in pnpm pn pnpx pnx; do ln -s "/opt/pnpm/$bin" "/usr/local/bin/$bin"; done

WORKDIR /app

COPY package.json pnpm-lock.yaml pnpm-workspace.yaml* ./

RUN pnpm install --frozen-lockfile

COPY . .

RUN pnpm build

FROM nginxinc/nginx-unprivileged:1.29.5-alpine-slim AS runtime

COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /app/dist/pixora-frontend/browser /usr/share/nginx/html

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
