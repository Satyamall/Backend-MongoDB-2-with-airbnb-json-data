
# Import Json data file in dbs of mongoDB:

- mongoimport --db airbnb --collection listing --file airbnb.json --port 27017
**shows:-** 2022-02-07T12:41:29.135+0530    connected to: mongodb://localhost:27017/
2022-02-07T12:41:31.138+0530    5555 document(s) imported successfully. 0 document(s) failed to import.

# show database
- show dbs
dmin     41 kB
airbnb  54.7 MB
config   111 kB
local   73.7 kB
masai    274 kB

# use database airbnb
- use airbnb
switched to db airbnb
airbnb>

# show collections
- show collections
listing

** Below Picture clear for mongoimport tools and file path for import **
-195

# find listing data
- db.listing.find()
show all data in listing of airbnb database

-db.listing.find().count()
5555

# db.listing.find({'address.country_code':"US" })
-196
-197

# db.listing.find({'address.country_code':"US" },{'address.country_code': 1})

[
  { _id: '10021707', address: { country_code: 'US' } },
  { _id: '10057826', address: { country_code: 'US' } },
  { _id: '1001265', address: { country_code: 'US' } },
  { _id: '1003530', address: { country_code: 'US' } },
  { _id: '10096773', address: { country_code: 'US' } },
  { _id: '10120414', address: { country_code: 'US' } },
  { _id: '10133350', address: { country_code: 'US' } },
  { _id: '10166986', address: { country_code: 'US' } },
  { _id: '10166883', address: { country_code: 'US' } },
  { _id: '10227000', address: { country_code: 'US' } },
  { _id: '1022200', address: { country_code: 'US' } },
  { _id: '10266175', address: { country_code: 'US' } },
  { _id: '10138784', address: { country_code: 'US' } },
  { _id: '10140368', address: { country_code: 'US' } },
  { _id: '10332161', address: { country_code: 'US' } },
  { _id: '102995', address: { country_code: 'US' } },
  { _id: '10280433', address: { country_code: 'US' } },
  { _id: '103161', address: { country_code: 'US' } },
  { _id: '10317142', address: { country_code: 'US' } },
  { _id: '1042446', address: { country_code: 'US' } }
]

#  db.listing.find({'address.country_code':"US" },{'address.country_code': 1, name: 1})
[
  {
    _id: '10021707',
    name: 'Private Room in Bushwick',
    address: { country_code: 'US' }
  },
  {
    _id: '10057826',
    name: 'Deluxe Loft Suite',
    address: { country_code: 'US' }
  },
  {
    _id: '1001265',
    name: 'Ocean View Waikiki Marina w/prkg',
    address: { country_code: 'US' }
  },
  {
    _id: '1003530',
    name: 'New York City - Upper West Side Apt',
    address: { country_code: 'US' }
  },
  {
    _id: '10096773',
    name: 'Easy 1 Bedroom in Chelsea',
    address: { country_code: 'US' }
  },

** Below Picture clear above **
  -198
  -199

# db.listing.find({'address.country_code':"US" },{_id: 0,'address.country_code': 1, name: 1})
[
  { name: 'Private Room in Bushwick', address: { country_code: 'US' } },
  { name: 'Deluxe Loft Suite', address: { country_code: 'US' } },
  {
    name: 'Ocean View Waikiki Marina w/prkg',
    address: { country_code: 'US' }
  },
  {
    name: 'New York City - Upper West Side Apt',
    address: { country_code: 'US' }
  },
  {
    name: 'Easy 1 Bedroom in Chelsea',
    address: { country_code: 'US' }
  },
 
# db.listing.find({'address.country_code':"US" },{_id: 0,'address.country_code': 1, name: 1}).count()
1222

# db.listing.find({'address.country_code':"US" },{_id: 0,'address.country_code': 1, name: 1, review_scores: 1}).limit(1)
[
  {
    name: 'Private Room in Bushwick',
    address: { country_code: 'US' },
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 8,
      review_scores_value: 8,
      review_scores_rating: 100
    }
  }
]

** Below Picture Clear the above command **
-200

# db.listing.find({'address.country_code':"US", 'review_scores.review_scores_rating': {$gte: 85}},{_id: 0,'address.country_code': 1, name: 1, review_scores: 1}).limit(1)
[
  {
    name: 'Private Room in Bushwick',
    address: { country_code: 'US' },
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 8,
      review_scores_value: 8,
      review_scores_rating: 100
    }
  }
]

** Below Picture for above **
-201
-202

# db.listing.find({'address.country_code':"US", 'review_scores.review_scores_rating': {$gte: 85}},{_id: 0,address: 1, name: 1, review_scores: 1})
[
  {
    name: 'Private Room in Bushwick',
    address: {
      street: 'Brooklyn, NY, United States',
      suburb: 'Brooklyn',
      government_area: 'Bushwick',
      market: 'New York',
      country: 'United States',
      country_code: 'US',
      location: {
        type: 'Point',
        coordinates: [ -73.93615, 40.69791 ],
        is_location_exact: true
      }
    },

# $or:
- db.listing.find({ $or: [{'address.country_code':"US"}]},{_id: 0,address: 1, name: 1, review_scores: 1})
[
  {
    name: 'Private Room in Bushwick',
    address: {
      street: 'Brooklyn, NY, United States',
      suburb: 'Brooklyn',
      government_area: 'Bushwick',
      market: 'New York',
      country: 'United States',
      country_code: 'US',
      location: {
        type: 'Point',
        coordinates: [ -73.93615, 40.69791 ],
        is_location_exact: true
      }
    },

** Below Picture for above **
-203

# db.listing.find({ $or: [{'address.country_code': "CA"},{'address.country_code':"US"}]},{_id: 0,address: 1, name: 1, review_scores: 1})
[
  {
    name: 'Private Room in Bushwick',
    address: {
      street: 'Brooklyn, NY, United States',
      suburb: 'Brooklyn',
      government_area: 'Bushwick',
      market: 'New York',
      country: 'United States',
      country_code: 'US',
      location: {
        type: 'Point',
        coordinates: [ -73.93615, 40.69791 ],
        is_location_exact: true
      }
    },
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 8,
      review_scores_value: 8,
      review_scores_rating: 100
    }
  },
  {
    name: 'Modern Spacious 1 Bedroom Loft',
    address: {
      street: 'Montréal, Québec, Canada',
      suburb: 'Mile End',
      government_area: 'Le Plateau-Mont-Royal',
      market: 'Montreal',
      country: 'Canada',
      country_code: 'CA',
      location: {
        type: 'Point',
        coordinates: [ -73.59111, 45.51889 ],
        is_location_exact: true
      }
    },
    review_scores: {}
  },

# db.listing.find({ $or: [{'address.country_code': "CA"},{'address.country_code':"US"}]},{_id: 0,address: 1, name: 1, review_scores: 1}).count()
1871

** Below picture for above **
-204

# db.listing.find({ $or: [{'address.country_code': "CA"},{'review_scores.review_scores_rating': {$gte: 99}}]},{_id: 0,address: 1, name: 1, review_scores: 1})
[
  {
    name: 'Private Room in Bushwick',
    address: {
      street: 'Brooklyn, NY, United States',
      suburb: 'Brooklyn',
      government_area: 'Bushwick',
      market: 'New York',
      country: 'United States',
      country_code: 'US',
      location: {
        type: 'Point',
        coordinates: [ -73.93615, 40.69791 ],
        is_location_exact: true
      }
    },
    review_scores: {
      review_scores_accuracy: 10,
      review_scores_cleanliness: 10,
      review_scores_checkin: 10,
      review_scores_communication: 10,
      review_scores_location: 8,
      review_scores_value: 8,
      review_scores_rating: 100
    }
  },

# $and: 
-db.listing.find({ $and: [{ 'address.country_code': "CA" }, { 'review_scores.review_scores_rating': { $gte: 99 } }] }, { _id: 0, address: 1, name: 1, review_scores: 1 }).count()
162

** Below Picture for above **
-205

# db.listing.find({ $and: [{ 'address.country_code': "CA" }, { $or: [{ 'review_scores.review_scores_rating': 100},{'review_scores.review_scores_rating': 99}] }] }, { _id: 0, address: 1, name: 1, review_scores: 1 }).count()
162

#  db.listing.find({ $and: [{ 'address.country_code': "CA" }, { $or: [{ 'review_scores.review_scores_rating': 100},{'review_scores.review_scores_rating': 100}] }] }, { _id: 0, address: 1, name: 1, review_scores: 1 }).count()
146

# db.listing.find({ $and: [{ 'address.country_code': "CA" }, { $or: [{ 'review_scores.review_scores_rating': 99},{'review_scores.review_scores_rating': 99}] }] }, { _id: 0, address: 1, name: 1, review_scores: 1 }).count()
16

** Below picture for above ** 
-206


# $not:
-  db.listing.find({'address.country_code': {$not: {$eq: "US"}} })

- db.listing.find({'address.country_code': {$not: {$eq: "US"}} }).count()
4333

# $eq:
-db.listing.find({'address.country_code': {$eq: "US"} }).count()
1222

# db.listing.find({'address.country_code': {$eq: "US"},'amenities.0': 'Wifi' },{ameneties: 1}).count()  
115

#  db.listing.find({'address.country_code': {$eq: "US"},'amenities.0': 'Wifi' },{amenities: 1})

** Below picture for above **
-208

# db.listing.find({'address.country_code': {$eq: "US"},'amenities':{$all:['Wifi', 'Shampoo' ]}},{amenities: 1})
show all data matches 'Wifi' and 'Shampoo'

#  db.listing.find({'address.country_code': {$eq: "US"},'amenities':{$all:['Wifi', 'Shampoo' ]}},{amenities: 1}).count()
857

** Below Picture show all above **
-209

# db.listing.find({'address.country_code': {$eq: "US"},'amenities':{$size: 10}},{amenities: 1}).count() 
29

# db.listing.find({'address.country_code': {$eq: "US"},'amenities':{$size: 10}},{amenities: 1}) 

# it show in amenities part only 10 data:
[
  {
    _id: '10021707',
    amenities: [
      'Internet',
      'Wifi',
      'Air conditioning',
      'Kitchen',
      'Buzzer/wireless intercom',
      'Heating',
      'Smoke detector',
      'Carbon monoxide detector',
      'Essentials',
      'Lock on bedroom door'
    ]
  },

** Below picture show all above data **
-210

#  $ elemMatch:
- db.listing.find({'address.country_code': {$eq: "US"}}, {'reviews':{$elemMatch: {reviewer_name: "Richard"}} })
[
  { _id: '10021707' },
  { _id: '10057826' },
  { _id: '1001265' },
  { _id: '1003530' },
  { _id: '10096773' },
  { _id: '10120414' },
  { _id: '10133350' },
  { _id: '10166986' },
  { _id: '10166883' },
  { _id: '10227000' },
  { _id: '1022200' },
  { _id: '10266175' },
  { _id: '10138784' },
  { _id: '10140368' },
  { _id: '10332161' },
  { _id: '102995' },
  { _id: '10280433' },
  { _id: '103161' },
  { _id: '10317142' },
  {
    _id: '1042446',
    reviews: [
      {
        _id: '30874295',
        date: ISODate("2015-04-28T04:00:00.000Z"),
        listing_id: '1042446',
        reviewer_id: '29341675',
        reviewer_name: 'Richard',
        comments: 'This is a great place to stay, we really liked the condo and the property, particularly the ability to walk out onto the beach.  Very quiet, just a few folks strolling the beaches, nice change from Kaanapali.   \r\n' +
          '\r\n' +
          'The room is very private, with only palms and ocean outside the windows.  The small park area next door is nice as well.\r\n' +
          '\r\n' +
          'The condo is comfortable with everything you need.   Will be hoping to come back in the future.'   
      }
    ]
  }
]

** Below picture for above **
-211

# it
[
  { _id: '10392282' },
  { _id: '10527243' },
  {
    _id: '10548991',
    reviews: [
      {
        _id: '409800953',
        date: ISODate("2019-02-08T05:00:00.000Z"),
        listing_id: '10548991',
        reviewer_id: '172617335',
        reviewer_name: 'Richard',
        comments: '非常棒的体验,非常棒的房东,干净整洁, 设施齐全｡强烈推荐｡'
      }
    ]
  },
  ..........................
 ..........................
 .............................

** Below picture for above **
-212

# db.listing.find({'address.country_code': {$eq: "US"}}, {'reviews':{$elemMatch: {reviewer_name: "Richard"}} },{_id: 0, reviews: 1}).limit(1)
[ { _id: '10021707' } ]

# db.listing.find({'address.country_code': {$eq: "US"}, 'reviews':{$elemMatch: {reviewer_name: "Richard"}}},{_id: 0, reviews: 1}).limit(1)
[
  {
    reviews: [
      {
        _id: '30874295',
        date: ISODate("2015-04-28T04:00:00.000Z"),
        listing_id: '1042446',
        reviewer_id: '29341675',
        reviewer_name: 'Richard',
        comments: 'This is a great place to stay, we really liked the condo and the property, particularly the ability to walk out onto the beach.  Very quiet, just a few folks strolling the beaches, nice change from Kaanapali.   \r\n' +
          '\r\n' +
          'The room is very private, with only palms and ocean outside the windows.  The small park area next door is nice as well.\r\n' +
          '\r\n' +
          'The condo is comfortable with everything you need.   Will be hoping to come back in the future.'   
      },
      .................
      ............
      ......

# db.listing.find({'address.country_code': {$eq: "US"}, 'reviews':{$elemMatch: {reviewer_name: "Richard"}}},{_id: 0, reviews: {$elemMatch: {reviewer_name: "Richard"}}}).limit(1)
[
  {
    reviews: [
      {
        _id: '30874295',
        date: ISODate("2015-04-28T04:00:00.000Z"),
        listing_id: '1042446',
        reviewer_id: '29341675',
        reviewer_name: 'Richard',
        comments: 'This is a great place to stay, we really liked the condo and the property, particularly the ability to walk out onto the beach.  Very quiet, just a few folks strolling the beaches, nice change from Kaanapali.   \r\n' +
          '\r\n' +
          'The room is very private, with only palms and ocean outside the windows.  The small park area next door is nice as well.\r\n' +
          '\r\n' +
          'The condo is comfortable with everything you need.   Will be hoping to come back in the future.'   
      }
    ]
  }
]


