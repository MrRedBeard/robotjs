Updated python, node, dependenices
Added missing "#include <string.h>" to xdisplay.c

rm -rf node_modules package-lock.json build prebuilds

sudo apt update;

sudo apt install -y \
  build-essential \
  pkg-config \
  python3 \
  make \
  g++ \
  libx11-dev \
  libxtst-dev \
  libpng-dev \
  libpng++-dev \
  zlib1g-dev \
  python3-pip python3-setuptools;

sudo npm install -g node-gyp@12.1.0;

npm install

export npm_config_node_gyp="$(command -v node-gyp)";
export npm_config_python="$(command -v python3)";

npm ci;

# Force build even if prebuilds exist
npm install --build-from-source;

# Or explicit rebuild
node-gyp rebuild;

npm run prebuild-linux-x64;

ls -la prebuilds/;
rm -rf build node_modules;

npm ci;

node -e "require('./'); console.log('loaded ok');";

node -e "const r=require('./'); console.log('mouse', r.getMousePos());";

git tag v0.6.21