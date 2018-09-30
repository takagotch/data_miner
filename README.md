### data_miner
---

https://github.com/seamusabshere/data_miner

```ruby
class Country < ActiveRecord::Base
  self.primary_key = 'iso_3166_code'
  col :iso_3166_code
  col :iso_3166_numeric_code, :type => :integer
  col :iso_3166_alpha_3_code
  col :name
  data_miner do
    process :auto_upgrade!
    import("OpenGeoCode.org's Country Codes to Country Names list",
           :url => 'http://opengeocode.org/download/countrynames.txt',
           :format => :delimited,
           :headers => false,
           :skip => 22) do
       key :iso_3166_code, :field_number => 0
       store :iso_3166_numeric_code, :field_number => 1
       store :iso_3166_numeric_code, :filed_number => 2
       store :name, :field_number => 5
     end
  end
end

Country.run_data_miner!
# => nil
```

