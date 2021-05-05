# SportsIcon Metadata Specifications


## Rationale

Metadata specifications that will be used for SportsIcon messages, these are a baseline for our usages of [dynamic NFTs](https://github.com/trustenterprises/hedera-dnft-specification). This will enable us to create Tokens and then attach messages through a topic this process used the [Hedera Consensus Service (HCS)](https://hedera.com/consensus-service) 

These meta specifications are used for to provide informal structure to the unstructured nature of posting messages. The type of messages include but are not exclusive to:

- Media metadata
- Athlete metadata 

We aren't including anti-piracy and 2-way links at this time. 

## The Data Flow

Read up on [dynamic NFTs](https://github.com/trustenterprises/hedera-dnft-specification) to understand the process but we have a base format which connects a token to a HCS topic.

This is the proposed dNFT name memo format, within 100 bytes.

- The Topic Id of the HCS topic
- The Account ID of SportsIcon
- The Symbol of the proposed
- Optional metadata to describe the dNFT

This could have this generic form below:

    'SI:{topic_id}:{account_id}'

We may explore using [DIDs](https://www.w3.org/TR/did-core/) as part of the memo, but that is low priority.

## Metadata Base Specification

Below is the basic format for a SportsIcon metadata message. A message must:

- Have a **version** which is numeric for a given schematype
- Have a **schematype** which describes the type of metadata, so we can process the data
- Have **data** which conforms to the **schematype**
- Have a **ts** in epoch format which describes the change of state.  

```
{
    "version": "1",
    "schematype": "athlete|media",
    "data": {},
    "ts": 0      
}
```

### Athlete Metadata

An athlete is an entity which describes an individual athlete, this is the payload which is present inside of the **data** field. 

- Have a **name** of the athlete
- Have a **resource** which connects to the SportsIcon athlete resource as a url 

```
{
    "name": "Matt Smithies",
    "resource": "{{domain}}/athlete/1" 
}
```
 

### Media

Media is content that is linked to a NFT token, in the basic form content is a url from a NFT to a IPFS and s3 URL in the future we will add capacity for the media to link back to the NFT through the use of Exif metadata tags to generate a unique hash.  

- Have a **cid** of the ipfs storage [content addressing](https://docs.ipfs.io/concepts/content-addressing/#identifier-formats)
- Have a **s3** link which is a link to media through SportIcons AWS

```
{
    "cid": "QmbWqxBEKC3P8tqsKc98xmWNzrzDtRLMiMPL8wBuTGsMnR",
    "s3": "{{s3 public url}}"
}
```
