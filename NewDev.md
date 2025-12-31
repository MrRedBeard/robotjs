rm -rf node_modules package-lock.json;
npm install;

npm i -D node-gyp@^11;

npm i -D @electron/rebuild@latest;

npm_config_python=/usr/bin/python3.13 \
npm_config_node_gyp="$(pwd)/node_modules/node-gyp/bin/node-gyp.js" \
npx node-gyp --version;
npm install;

npm config get node_gyp;
npm config get python;

npm run prebuild
npm run install