### Gift Cards v2.1 Features and Use cases
  - Gift cards and respective denominations along with basic item details including terms and conditions comes as part of on_search (to facilitate cached searches)
  - Types of gift cards items (categories) - 
      - Card code (5000 rupees gift card applied on target purchase(s))
      - Deal/ Promo code (50% discount on the target purchase)
      - Online e-pay (brand/ OEM wallet)
      - E-RUPI (e-rupi gift cards)
  - Types of fulfilment
      - Fulfilled by seller app
      - Fulfilled by buyer app
  - Categories of gift cards based on industry in ITEM_DETAILS tag group. Refer the enums for the list.
  - Provision of gift card code (and PIN) in the protocol (mandatory for buyer app fulfilment type)
      - Enablement of encryption for the same - flow here
      - Added instructions in the stops object for any specific instructions around the usage of the gift code/ PIN
  - Provision of gift card redemption link (as part of on_status)
  - Alternate commercial model available [here](https://docs.google.com/document/d/1R6A84h6Rn21ezRBwLcsD81miOnAsFvtxiJdzP1yml3M/edit?usp=sharing).
  - Illustrations of seller app collecting payment
  - Illustration for invalid contact detail shared for seller app fulfillment type
    - Seller app canceling the order
    - Seller app seeking update on the contact information of the buyer
  - Enablement of physical store based gift cards 
    
### Technical salient features
  - “offered_value” attribute in item.price signifying the worth of the gift card, while the “value” provides the price of the gift card
  -  Expiration of gift cards has been handled through the item.time object
  - Selection of type of fulfillment type is as part of /select call, selected by buyer/ buyer app
  - Fulfillment elaboration for multiple quantities and multiple gift cards in single order, where each quantity has a respective       fulfillment associated
    - Partial cancellation at gift card quantity level
  - Addition of error codes
    - Seller app not servicing for particular contact info or location
    - Seller app not supporting fulfillment at their end
  - Included tags for usability, partial redemption and clubbing of gift cards
  - Schema updates  (viz. image object) to align with the core schema

### Flow for physical store based gift cards
 
- Buyer app requests for catalog for a particular city
- Seller app responds with their catalog comprising of online as well as offline gift cards
  - Locations shared for respective stores for which gift cards are provided, including of serviceability (illustrated through circle in the examples) 
  - Items that based on specific stores are mapped to their respective locations
- Buyer app renders gift cards based on the buyer’s location and the serviceability provided by the seller apps
- For gift cards that are mapped to specific locations, once selected, the buyer’s location is shared over the /select call 
- Seller app responds with a quote if serviceable, otherwise error if not serviceable
- Rest of the flow remains the same (with the incorporation of the location of the buyer)


   

    

   
