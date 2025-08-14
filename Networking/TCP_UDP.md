## TCP (Transmission Control Protocol)

Goal → Reliable communication between two devices.

Main features:

Guarantees that data arrives in order and without loss.

Resends lost packets automatically.

Uses three-way handshake to establish a connection before sending data.

Slower than UDP because of error checking and acknowledgments.

Best for:

Web browsing (HTTP/HTTPS)

Email (SMTP, IMAP)

File transfers (FTP)

Anything where missing data breaks the whole thing.

## UDP (User Datagram Protocol)

Goal → Send data fast, even if some of it is lost.

Main features:

No connection — just send the data and hope it arrives.

No guarantee of order or delivery.

No automatic retransmission.

Much faster and lighter than TCP.

Best for:

Live video/audio streaming

Online gaming

DNS lookups

Anything where speed matters more than perfection.
