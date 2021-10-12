Agent Feed Format Specification
===============================

Introduction
------------

Specification of JSON format for submitting an automated agent roster to Who's Who in Luxury Real Estate.

Example JSON
------------

```json
{
  "Agent": [
    {
      "JobTitle": "VP of Sneezing",
      "Media": [
        {
          "MediaCategory": "Profile Photo",
          "MediaModificationTimestamp": "2018-09-20 13:53:38 UTC",
          "MediaURL": "http://mydomain.com/mug.jpg"
        },
        {
          "MediaCategory": "Background Photo",
          "MediaModificationTimestamp": "2018-09-20 13:53:38 UTC",
          "MediaURL": "http://mydomain.com/background.jpg"
        },
        {
          "MediaCategory": "Video",
          "MediaModificationTimestamp": "2018-09-20 13:53:38 UTC",
          "MediaURL": "http://mydomain.com/video.mpg"
        }
      ],
      "MemberAddress1": "2110 Western Avenue",
      "MemberAddress2": null,
      "MemberCity": "Seattle",
      "MemberCountry": "US",
      "MemberCounty":"King",
      "MemberDescription": [
        {
          "remark": "I like sneezing, code, and Oxford commas.", 
          "languageCode": "en"
         }
       ],
      "MemberDirectPhone": "555-123-4567",
      "MemberEmail": "sneezer@luxre.com",
      "MemberFirstName": "Michael",
      "MemberKey": "LRE001",
      "MemberLanguages": [
        "en",
        "sv"
      ],
      "MemberLastName": "Edlund",
      "MemberMlsId": [
        "12345678",
        "MLSID123"
      ],
      "MemberMobilePhone": "555-1235050",
      "MemberOfficePhone": "555-3129090",
      "MemberOfficePhoneExt": null,
      "MemberPassword": null,
      "MemberPostalCode": "98121",
      "MemberPreferredPhone": "206-9879090",
      "MemberPreferredPhoneExt": null,
      "MemberLicenses": [
        {
          "number": "01424267",
          "stateCode": "CA"
        }
      ],
      "MemberStateOrProvince": "WA",
      "MemberTollFreePhone": "800-9879090",
      "ModificationTimestamp": "2018-09-20 13:53:38 UTC",
      "OfficeKey": "OFF123",
      "SocialMedia": [
        {
          "SocialMediaType": "Twitter",
          "SocialMediaUrlOrId": "@arcticleo"
         },
         {
          "SocialMediaType": "LinkedIn",
          "SocialMediaUrlOrId": "https://www.linkedin.com/in/arcticleo/"
        },
        {
          "SocialMediaType": "Website",
          "SocialMediaUrlOrId": "http://myownsite.com"
        }
      ]
    }
  ]
}
```

Field Descriptions
------------------

### Agent

Top level object. Contains an array of objects with the following attributes.

**JobTitle** — _String(50)_

The title or position of the agent within their organization.

**MemberAddress1** — _String(50)_

The street number, direction, name and suffix of the agent.

**MemberAddress2** — _String(50)_

The unit/suite number of the agent.

**MemberCity** — _String(50)_

The city of the agent.

**MemberCountry** — _String(2)_

The two digit country abbreviation of the agent's postal address.

**MemberCounty** — _String(50)_

The county of the agent.

**MemberDescription** — _String(8000)_

The bio/description of the agent.

**MemberDirectPhone** — _String(16)_

North American 10 digit phone numbers should be in the format of ###-###-#### (separated by hyphens). Other conventions should use the common local standard.

**MemberEmail** — _String(80)_

The email address of the agent.

**MemberFirstName** — _String(50)_

The first name of the agent.

**MemberKey** — _String(255)_

A unique string identifier for the agent.

**MemberLanguages** — _Array of String(50)_

An array with the ISO 639-1 codes of languages spoken by the agent.

**MemberLastName** — _String(50)_

The last name of the agent.

**MemberMlsId** — _Array of String(25)_

The identifiers for the MLSs that the agent is associated with.

**MemberMobilePhone** — _String(16)_

North American 10 digit phone numbers should be in the format of ###-###-#### (separated by hyphens). Other conventions should use the common local standard.

**MemberOfficePhone** — _String(16)_

North American 10 digit phone numbers should be in the format of ###-###-#### (separated by hyphens). Other conventions should use the common local standard.

**MemberOfficePhoneExt** — _String(10)_

The extension of the given phone number (if applicable).

**MemberPassword** _String(25)_

If provided, the seed password that the agent's user will initially have. If left blank, a random password will be created and emailed to the agent's user.

**MemberPostalCode** — _String(10)_

The postal code of the agent.

**MemberPreferredPhone** — _String(16)_

North American 10 digit phone numbers should be in the format of ###-###-#### (separated by hyphens). Other conventions should use the common local standard.

**MemberPreferredPhoneExt** —  _String(10)_

The extension of the given phone number (if applicable).

**MemberLicenses** — _Array of JSON objects_

number: String(50) - The license.
stateCode: String(2) - The state in which the member is licensed.

**MemberStateLicenseState** — _String(3)_

The ISO 3166-2 code for the state or province in which the member is licensed.

**MemberTollFreePhone** — _String(16)_

North American 10 digit phone numbers should be in the format of ###-###-#### (separated by hyphens). Other conventions should use the common local standard.

**ModificationTimestamp** — _Timestamp String(27)_

Timestamp for when the agent record was last modified.

**OfficeKey** — _String(255)_

A unique string identifier for the office where the agent hangs their license.


### Media

The Media Resource is a representation of agent profile photos and videos.

**MediaCategory** — _String(50)_

Category describing the photo. 

Allowed values: 

- Profile Photo
- Background Photo
- Video

**MediaModificationTimestamp** — _Timestamp String(27)_

Timestamp for when the photo was last updated. Update this value when a photo has changed but maintains the same name.

**MediaURL** — _String(8000)_

The URI to the photo file referenced by this object.

### SocialMedia

A collection of social media objects that is related to the agent.

**SocialMediaType** — _String(50)_

The type of sites, blog, social media, the Member URL or ID is referring to. 

Allowed values:

- Facebook
- Instagram
- LinkedIn
- Pinterest
- Skype
- Twitter
- Website

**SocialMediaUrlOrId** — _String(8000)_

The website URL or ID of social media site or account that the Social Media Type is referring to. 






