# FaunaDB: Sample DB



#### Table of Contents
* [Schema](#schema)
* [Query Reference](#query-reference)

## Schema

The schema represents the data model for a simple E-Commerce application.

![alt text](images/ecommerce.svg "E-Commerce Schema")


## Query Reference

### Warehouse

<table>
  <tr>
    <th>Operation</th>
    <th>FQL</th>
    <th>GraphQL</th>
  </tr>
  <tr>
    <td>Create Warehouse</td>
    <td>
        <pre>
Create(
  Class("Warehouse"), { 
    data: { 
      "name": "East", 
      "address": { 
        "street": "13 Pierstorff Drive", 
        "city": "Washington",
        "state": "DC",
        "zipCode": "20220"
      }
    }
  }
);
		</pre>
    </td>
    <td>
      <pre>
mutation {
	createWarehouse(data: {
    name: "East"
    address: {
      street: "13 Pierstorff Drive"
      city: "Washington"
      state: "DC"
      zipCode: "20220"
    }
  }){
    _id
  }
}
		</pre>
    </td>
  </tr>
  <tr>
    <td>

    </td>
    <td>
    </td>
  </tr>
</table>

