# http2-frame-test-case

Test cases to encode/decode [http2](http://tools.ietf.org/html/draft-ietf-httpbis-http2) frame.

## Test case files

Each directory has test cases of its corresponding frame.
For example, "data" directory has test cases of the DATA frame.
Each JSON file is named #{n}.json. n is 0 origin.

## JSON Format

Each JSON file has:

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

First, decode a JSON file to data structures in your programming language.
For simplicity, we refer to such data structures just by JSON names, such as
"frame".

To decode "wire", you MUST use default setting values of HTTP2 and an empty dynamic table of HPACK.

### Normal cases

"frame" is not null and "error" is null.

1. Decode "wire" to obtain a decoded frame. Then, compare the decoded frame with "frame".
2. Encode the decode frame to obtain an encoded frame. Then, compare the encoded frame with "wire".

For the HEADERS frame,
"header_block_fragment" is carefully created just by using the static table.
If you decode "header_block_fragment" in step 1 and encode again in step 2,
you would obtain a different "wire"
since encoding algorithms of HPACK is not unique,

### Error cases

"frame" is null and "error" is not null.

1. Decode "wire" to obtain an error code. Then check if the error code is a member of "error".

## Contribution

- Please send a pull request with #{non-number}.json
- We will merge it by renaming it to #{latest}.json


## License

See [LICENSE](LICENSE) file
