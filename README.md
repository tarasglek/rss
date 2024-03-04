docker run --rm --user=$(id -u):$(id -g) --name cloudflared-tunnel -ti \
-e HOME=$HOME -v $HOME:$HOME -w $HOME cloudflare/cloudflared:latest login
docker run --rm --user=$(id -u):$(id -g) --name cloudflared-tunnel -ti  -e HOME=$HOME -v $HOME:$HOME -w $HOME cloudflare/cloudflared:latest tunnel create miniflux.glek.net
docker run --rm --user=$(id -u):$(id -g) --name cloudflared-tunnel -ti  -e HOME=$HOME -v $HOME:$HOME -w $HOME cloudflare/cloudflared:latest tunnel route dns miniflux.glek.net miniflux.glek.net
docker run --rm --user=$(id -u):$(id -g) --name cloudflared-tunnel -ti  -e HOME=$HOME -v $HOME:$HOME -w $HOME cloudflare/cloudflared:latest tunnel --config $HOME/.cloudflared/tunnel-config.json run
tar -c dot_cloudflared/ | sops -e /dev/stdin  > dot_cloudflared.tar.sops
sops -e .env > .env.enc
