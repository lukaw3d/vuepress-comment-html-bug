If I `vuepress build` an index.md with:
```
text
<!-- comment -->
<a>html</a>
text
```
JavaScript breaks in a browser:
`DOMException: Failed to execute 'appendChild' on 'Node': This node type does not support this method.`

### Reproduce repo
```sh
npm i
npx vuepress build ./docs
npx http-server -c-1 ./docs/.vuepress/dist
```
Open http://127.0.0.1:8080/index
- Chrome throws `DOMException: Failed to execute 'appendChild' on 'Node': This node type does not support this method.`
- Firefox throws `DOMException: Node.appendChild: Cannot add children to a Text`
