# http2-frame-test-case

Test cases to encode/decode [http2](http://tools.ietf.org/html/draft-ietf-httpbis-http2) frame.

## Test case files

Each directory has test cases of its corresponding frame.
For example, "data" directory has test cases of DATA frame.
Each json file is named #{n}.json. n is 0 origin.

## JSON Format

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

Each property name is lower snake case (connected by underscore) of original name

### Example: a data frame

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

## Test algorithm

First, dcode a JOSN file to data structures of your programming language.
For simplicity, we refer such data structures just by JSON names, such as
"frame".

### Normal cases

"frame" is not null and "error" is null.

1. Decode "wire" to obtain a decoded frame. Then, compare the decoded frame with "frame".
2. Encode the decode frame to obtain an encoded frame. Then, compare the encoded frame with "wire".

### Error cases

"frame" is null and "error" is not null.

## Contribution

- Please send a pull request with #{non-number}.json
- We will merge it by renaming it to #{latest}.json


## License

see LICENSE file
