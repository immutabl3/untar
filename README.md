# untar

a fast, browser-oriented tarball manipulation with zero dependencies

## why?

this is a port of [tarballjs](https://github.com/ankitrohatgi/tarballjs), which was failing in Next.js/modern build systems, both because of a lack of proper UMD and node support. The project structure also doesn't support tree-shaking 

## usage

### `untar`

takes an [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) and returns an array of `entries` representing files and folders

```js
import { untar } from '@immutabl3/tar';
const res = await fetch(url);
const buffer = await res.arrayBuffer();
const entries = await untar(buffer);
```

Entry
* `.path`: _string_ - file's tar path
* `.ext`: _string_ - file's extension (e.g. `png`, `jpg`)
* `.type`: _string_ - 'file' or 'directory'
* `.size`: _number_ - file's byte size
* `.getText()`: _string_ - read the file as a text string
* `.getBinary()`: _Uint8Array_ - read the file as bytes
* `.getBlob(mimetype)`: _Blob_ - read the file as a Blob with the provided mime

## limitations

- File name (including path) has to be less than 100 characters.
- Maximum total file size seems to be limited to somewhere between 500MB to 1GB (exact limit is unknown).

## tests

* `npm install`
* `npm test`

## references

- https://en.wikipedia.org/wiki/Tar_(computing)
- https://www.gnu.org/software/tar/manual/html_node/Standard.html
