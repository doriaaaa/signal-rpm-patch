# signal-rpm-patch
I wrote this patch because Signal does not provide any native application on Fedora. 

First you need to clone the repository from Signal, then apply this patch by running
```
patch -p1 package.json < package.patch
```
Afterwards, you can build Signal from source.

Run the following commands:
```
rm -r node_modules
rm package-lock.json
rm yarn.lock
```
Also remove these two patches:
```
rm @types+express+4.17.18.patch
rm socks-proxy-agent-8.0.1.patch
```
Then build from source:
```
yarn cache clean
yarn install --frozen-lockfileyarn
yarn generate
yarn build-release
cd release/
sudo rpm -Uvh <the signal version you just built>
```
Reference: [Guide to compile Signal from source in Fedora Linux.](https://www.reddit.com/r/signal/comments/x9576c/guide_to_compile_signal_from_source_in_fedora/)
