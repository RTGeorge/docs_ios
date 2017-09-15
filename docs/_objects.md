# Objects
## Top level client library object

> Include the FoxDen client library and print out the version.
```swift
override open func send(_ element: DDXMLElement!) {
  // Override the sendElement to include our nickname XEP-0172
  if element.name == "presence" || element.name == "message" {
    let nickElement = DDXMLElement(name: "nick", xmlns: XMLNS_NICK)
    nickElement?.stringValue = nickname
    element.addChild(nickElement!)
  }

  if element.name == "presence" {
    for extra in additionalElements {
      element.addChild(DDXMLElement(name: extra.name, stringValue: extra.value))
    }
  }

  super.send(element)
}
```

The main entry point for the client library provides the operations as described in [Operations](#operations-object).

## Session Object

> Create a session with example data (returns not-authorized unless given valid token).
```swift
open func isUsersJid(_ jid :XMPPJID) -> Bool {
  if let resource = jid.resource , resource == xmppStream.uuid {
    return true
  }
        
  return jid.isEqual(to: xmppStream.myJID)
}
```

The session object is used to add and remove video & screen-share streams to a conference.
