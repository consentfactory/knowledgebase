# Viewing Transceivers 

To view transceivers as they're inserted into the firewall:

```
tail lines 100 follow yes cp-log brdagent.log
```

You can also `less` and `grep` the files, but you can't pipe the output `tail` to `grep` like in the Unix/Linux world. 

Blog Entry:
https://www.consentfactory.com/quickie-palo-alto-firewalls-and-transceivers/

Palo Alto details:
https://knowledgebase.paloaltonetworks.com/KCSArticleDetail?id=kA10g000000PN8fCAG

Also:
https://www.google.com/books/edition/Mastering_Palo_Alto_Networks/GCf4DwAAQBAJ?hl=en&gbpv=1&dq=palo+alto+logs+%22cp-log%22&pg=PA451&printsec=frontcover
