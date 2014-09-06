# http2-frame-test-case

test case for encode/decode http2 frame.

## Draft

http://tools.ietf.org/html/draft-ietf-httpbis-http2

## Directory

Each directory has testcase of its names frame.
For example, data directory has a test cases of DATA frame.

## File Name

Each json named #{n}.json. n is 0 origin.
If you add new testcase, increment number of file.

## JSON Format

To test the decoder implementation, for each story file, for each case
in ```cases``` in the order they appear, decode compressed header
block in ```wire``` and verify the result against the header set in
```headers```. Please note that elements in ```cases``` share the same
compression context.

To test the encoder implementation, generate json story files by
encoding header sets in ```headers```. Using json files in
```raw-data``` is handy. Then use your decoder to verify that it can
successfully decode the compressed header block. If you can play with
other HTTP2 decoder implementations, try decoding your encoded data
with them. If there is any mismatch, then there must be a bug in
somewhere either encoder or decoder, or both.

### Frame Header format

Each json has:

- draft: http2 draft version number of implementation.
- description: general description of implementation.
- cases: test cases.
  - seqno:  a sequence number. 0 origin.
  - wire:   encoded wire data in hex string.
  - length: length property of frame header.
  - type:   type property of frame header.
  - flags:  flags property of frame header.
  - stream_identifier: stream identifier property of frame header.
  - frame_payload: see frame payload section


### frame payload

each property names are lower snake case of original name

### example: headers frame

```js
{
  "draft": 14,
  "description": "expain your implementation",
  "cases": [
    {
      "seqno": 0,
      "wire": "1234567890abcdef",
      "length": 10,
      "type": 1,
      "flags": 1,
      "stream_identifier": 1,
      "frame_payload": {
        "palength": 10,
        "stream_dependency": 10,
        "weight": 10,
        "header_block_fragment": "1234567890abcdef",
        "padding": "00000000000"
      }
    },
    .....
  ]
}
```

## License

see LICENSE file
