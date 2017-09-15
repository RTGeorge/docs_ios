# Objects
## Top level client library object

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

## Session Object

```swift
open func isUsersJid(_ jid :XMPPJID) -> Bool {
  if let resource = jid.resource , resource == xmppStream.uuid {
    return true
  }
        
  return jid.isEqual(to: xmppStream.myJID)
}
```

