# NAME

Zing::Store::Redis - Redis Storage

# ABSTRACT

Redis Storage Abstraction

# SYNOPSIS

    use Zing::Store::Redis;
    use Zing::Encoder::Dump;

    my $redis = Zing::Store::Redis->new(
      encoder => Zing::Encoder::Dump->new
    );

    # $redis->drop;

# DESCRIPTION

This package provides a [Redis](https://metacpan.org/pod/Redis) storage adapter for use with data persistence
abstractions.

# INHERITS

This package inherits behaviors from:

[Zing::Store](https://metacpan.org/pod/Zing%3A%3AStore)

# LIBRARIES

This package uses type constraints from:

[Zing::Types](https://metacpan.org/pod/Zing%3A%3ATypes)

# ATTRIBUTES

This package has the following attributes:

## client

    client(InstanceOf["Redis"])

This attribute is read-only, accepts `(InstanceOf["Redis"])` values, and is optional.

# METHODS

This package implements the following methods:

## decode

    decode(Str $data) : HashRef

The decode method decodes the JSON data provided and returns the data as a hashref.

- decode example #1

        # given: synopsis

        $redis->decode('{"status"=>"ok"}');

## drop

    drop(Str $key) : Int

The drop method removes (drops) the item from the datastore.

- drop example #1

        # given: synopsis

        $redis->drop('zing:main:global:model:temp');

## encode

    encode(HashRef $data) : Str

The encode method encodes and returns the data provided as JSON.

- encode example #1

        # given: synopsis

        $redis->encode({ status => 'ok' });

## keys

    keys(Str @keys) : ArrayRef[Str]

The keys method returns a list of keys under the namespace of the datastore or
provided key.

- keys example #1

        # given: synopsis

        my $keys = $redis->keys('zing:main:global:model:temp');

- keys example #2

        # given: synopsis

        $redis->send('zing:main:global:model:temp', { status => 'ok' });

        my $keys = $redis->keys('zing:main:global:model:temp');

## lpull

    lpull(Str $key) : Maybe[HashRef]

The lpull method pops data off of the top of a list in the datastore.

- lpull example #1

        # given: synopsis

        $redis->lpull('zing:main:global:model:items');

- lpull example #2

        # given: synopsis

        $redis->rpush('zing:main:global:model:items', { status => 'ok' });

        $redis->lpull('zing:main:global:model:items');

## lpush

    lpush(Str $key, HashRef $val) : Int

The lpush method pushed data onto the top of a list in the datastore.

- lpush example #1

        # given: synopsis

        $redis->lpush('zing:main:global:model:items', { status => '1' });

- lpush example #2

        # given: synopsis

        $redis->lpush('zing:main:global:model:items', { status => '0' });

## recv

    recv(Str $key) : Maybe[HashRef]

The recv method fetches and returns data from the datastore by its key.

- recv example #1

        # given: synopsis

        $redis->recv('zing:main:global:model:temp');

- recv example #2

        # given: synopsis

        $redis->send('zing:main:global:model:temp', { status => 'ok' });

        $redis->recv('zing:main:global:model:temp');

## rpull

    rpull(Str $key) : Maybe[HashRef]

The rpull method pops data off of the bottom of a list in the datastore.

- rpull example #1

        # given: synopsis

        $redis->rpull('zing:main:global:model:items');

- rpull example #2

        # given: synopsis

        $redis->rpush('zing:main:global:model:items', { status => 1 });
        $redis->rpush('zing:main:global:model:items', { status => 2 });

        $redis->rpull('zing:main:global:model:items');

## rpush

    rpush(Str $key, HashRef $val) : Int

The rpush method pushed data onto the bottom of a list in the datastore.

- rpush example #1

        # given: synopsis

        $redis->rpush('zing:main:global:model:items', { status => 'ok' });

- rpush example #2

        # given: synopsis

        $redis->rpush('zing:main:global:model:items', { status => 'ok' });

        $redis->rpush('zing:main:global:model:items', { status => 'ok' });

## send

    send(Str $key, HashRef $val) : Str

The send method commits data to the datastore with its key and returns truthy.

- send example #1

        # given: synopsis

        $redis->send('zing:main:global:model:temp', { status => 'ok' });

## size

    size(Str $key) : Int

The size method returns the size of a list in the datastore.

- size example #1

        # given: synopsis

        my $size = $redis->size('zing:main:global:model:items');

- size example #2

        # given: synopsis

        $redis->rpush('zing:main:global:model:items', { status => 'ok' });

        my $size = $redis->size('zing:main:global:model:items');

## slot

    slot(Str $key, Int $pos) : Maybe[HashRef]

The slot method returns the data from a list in the datastore by its index.

- slot example #1

        # given: synopsis

        my $model = $redis->slot('zing:main:global:model:items', 0);

- slot example #2

        # given: synopsis

        $redis->rpush('zing:main:global:model:items', { status => 'ok' });

        my $model = $redis->slot('zing:main:global:model:items', 0);

## test

    test(Str $key) : Int

The test method returns truthy if the specific key (or datastore) exists.

- test example #1

        # given: synopsis

        $redis->rpush('zing:main:global:model:items', { status => 'ok' });

        $redis->test('zing:main:global:model:items');

- test example #2

        # given: synopsis

        $redis->drop('zing:main:global:model:items');

        $redis->test('zing:main:global:model:items');

# AUTHOR

Al Newkirk, `awncorp@cpan.org`

# LICENSE

Copyright (C) 2011-2019, Al Newkirk, et al.

This is free software; you can redistribute it and/or modify it under the terms
of the The Apache License, Version 2.0, as elucidated in the ["license
file"](https://github.com/iamalnewkirk/zing-store-redis/blob/master/LICENSE).

# PROJECT

[Wiki](https://github.com/iamalnewkirk/zing-store-redis/wiki)

[Project](https://github.com/iamalnewkirk/zing-store-redis)

[Initiatives](https://github.com/iamalnewkirk/zing-store-redis/projects)

[Milestones](https://github.com/iamalnewkirk/zing-store-redis/milestones)

[Contributing](https://github.com/iamalnewkirk/zing-store-redis/blob/master/CONTRIBUTE.md)

[Issues](https://github.com/iamalnewkirk/zing-store-redis/issues)
