#JSONPatch

Helper class that generates RFC 6902 compliant JSON patches.

This is what you want:

    [
        { "op": "test", "path": "/a/b/c", "value": "foo" },
        { "op": "remove", "path": "/a/b/c" },
        { "op": "add", "path": "/a/b/c", "value": [ "foo", "bar" ] },
        { "op": "replace", "path": "/a/b/c", "value": 42 },
        { "op": "move", "from": "/a/b/c", "path": "/a/b/d" },
        { "op": "copy", "from": "/a/b/d", "path": "/a/b/e" }
    ]

How to achieve that:

    NSArray *patches = [JSONPatch createPatch:^(JSONPatch* p){
    
        [p test:@"/a/b/c" value:@"foo"];
        [p remove:@"/a/b/c"];
        [p add:@"/a/b/c" value:@[@"foo",@"bar"]];
        [p replace:@"/a/b/c" value:@42];
        [p move:@"/a/b/c" to:@"/a/b/d"];
        [p copy:@"/a/b/d" to:@"/a/b/e"];
        
    }];

Serialize it to a JSON string (I suggest using Apple's excellent **NSJSONSerialization** class) and dinner's ready.

#Warning

JSON paths and values **ARE NOT** being checked.
That's something you would implement on the backend!

#License

JSONPatch is available under the MIT license. See the LICENSE file for more info.
