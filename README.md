[![Build Status](https://travis-ci.org/xaicron/p5-Net-APNs-HTTP2.svg?branch=master)](https://travis-ci.org/xaicron/p5-Net-APNs-HTTP2)
# NAME

Net::APNs::HTTP2 - APNs Provider API for Perl

# SYNOPSIS

    use Net::APNs::HTTP2;

    my $apns = Net::APNs::HTTP2->new(
        is_development => 1,
        auth_key       => 'auth_key.p8',
        key_id         => $key_id,
        team_id        => $team_id,
        bundle_id      => $bundle_id,
    );

    while (1) {
        $apns->prepare($device_token, {
            aps => {
                alert => 'some message',
                badge => 1,
            },
        }, sub {
            my ($header, $content) = @_;
            # $header = [
            #     ":status" => "200",
            #     "apns-id" => "82B34E17-370A-DBF4-5046-FF56A4EA1FAF",
            # ];
            ...
        });

        # You can chainged
        $apns->prepare(...)->prepare(...)->prepare(...);

        # send all prepared requests in parallel
        $apns->send;

        # do something
    }

    # must call `close` when finished
    $apns->close;

# DESCRIPTION

Net::APNs::HTTP2 is APNs Provider API for Perl.

# LICENSE

Copyright (C) xaicron.

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# AUTHOR

xaicron <xaicron@gmail.com>
