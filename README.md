# http2-frame-test-case

test case for encode/decode http2 frame.

## Draft

http://tools.ietf.org/html/draft-ietf-httpbis-http2

## JSON Format


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
