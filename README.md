# http2-frame-test-case

Test cases for encode/decode http2 frame.

## Draft

http://tools.ietf.org/html/draft-ietf-httpbis-http2

## Directory

Each directory has test cases of its corresponding frame.
For example, "data" directory has test cases of DATA frame.

## File Name

Each json is named #{n}.json. n is 0 origin.
If you add a new test case, increment the number of the file.

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

- description: general description of implementation.
- wire:   encoded wire data in hex string.
- frame:
  - length: length property of frame header.
  - type:   type property of frame header.
  - flags:  flags property of frame header.
  - stream_identifier: stream identifier property of frame header.
  - frame_payload: see frame payload section
- error:  a list of possible error codes


### frame payload

Each property name is lower snake case (connected by underscore) of original name

### example: a data frame

```js
{
    "error": null,
    "wire": "0000140008000000020648656C6C6F2C20776F726C6421486F77647921",
    "frame": {
        "length": 20,
        "frame_payload": {
            "data": "Hello, world!",
            "padding_length": 6,
            "padding": "Howdy!"
        },
        "flags": 8,
        "stream_identifier": 2,
        "type": 0
    },
    "description": "normal data frame"
}
```

## Contribution

- Please send a pull request with #{non-number}.json
- We will merge it by renaming it to #{latest}.json


## License

see LICENSE file
