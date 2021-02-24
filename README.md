If I `vuepress build` an index.md with:
```
text
<!-- comment -->
<a>html</a>
text
```
and publish it to https://lukaw3d.github.io/vuepress-comment-html-bug/index

JavaScript breaks in a browser:
`DOMException: Failed to execute 'appendChild' on 'Node': This node type does not support this method.`

### Reproduce repo
```sh
npm ci
npx vuepress build ./docs
npx http-server -c-1 ./docs/.vuepress/dist
```
Open http://127.0.0.1:8080/index
- Chrome throws `DOMException: Failed to execute 'appendChild' on 'Node': This node type does not support this method.`
- Firefox throws `DOMException: Node.appendChild: Cannot add children to a Text`

### No error
If I remove any one of those lines, it seems to work. Open these variants:
- http://127.0.0.1:8080/works1
- http://127.0.0.1:8080/works2
- http://127.0.0.1:8080/works3
- http://127.0.0.1:8080/works4

Everything seems to work in development version (`npx vuepress dev`)

### Vuepress info
```
$ npx vuepress info

Environment Info:

  System:
    OS: Linux 5.8 Ubuntu 20.04.2 LTS (Focal Fossa)
    CPU: (8) x64 Intel(R) Core(TM) i7-1065G7 CPU @ 1.30GHz
  Binaries:
    Node: 14.15.5 - /usr/bin/node
    Yarn: 1.22.5 - /usr/bin/yarn
    npm: 6.14.11 - /usr/bin/npm
  Browsers:
    Chrome: 88.0.4324.182
    Firefox: 85.0.1
  npmPackages:
    @vuepress/core:  1.8.2
    @vuepress/theme-default:  1.8.2
    vuepress: ^1.8.2 => 1.8.2
  npmGlobalPackages:
    vuepress: Not Found
```
