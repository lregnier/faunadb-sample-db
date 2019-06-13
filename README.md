# FaunaDB: Sample DB



#### Table of Contents
* [Schema](#schema)
* [Query Reference](#query-reference)
  * [Warehouse](#warehouse)

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
    <td valign="top"><b>Create a<br>Warehouse</b></td>
    <td valign="top">
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
    <td valign="top">
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
    <td valign="top"><b>Read a<br>Warehouse</b></td>
    <td valign="top">
      <pre>
Get(Ref(Class("Warehouse"), "1549398205020000"));
      </pre>
    </td>
    <td valign="top">
      <pre>
query {
  findWarehouseByID(id: "1549398205020000") {
    _id
    name
    address {
      street
      city
      state
      zipCode
    }
  }
}
      </pre>
    </td>
  </tr>
  <tr>
    <td valign="top"><b>Update a<br>Warehouse</b></td>
    <td valign="top">
     <pre>
Update(
  Ref(Class("Warehouse"), "1549398205020000"), {
    data: {
      "name": "North-East",
      "address": { 
        "street": "1 Corry Plaza", 
        "city": "Stockton",
        "state": "CA",
        "zipCode": "95205" 
      }
    }
  }
);
      </pre>
    </td>
    <td valign="top">
      <pre>
mutation {
  updateWarehouse(
    id: "1549398205020000",
  	data: {
    name: "North-East"
    address: {
      street: "1 Corry Plaz"
      city: "Stockton"
      state: "CA"
      zipCode: "95205"
    }
  }){
    _id
  }
}
      </pre>
    </td>
  </tr>
<tr>
    <td valign="top"><b>Delete a<br>Warehouse</b></td>
    <td valign="top">
     <pre>
Delete(Ref(Class("Warehouse"), "1549398205020000"))
      </pre>
    </td>
    <td valign="top">
      <pre>
mutation {
  deleteWarehouse(id: "235072781994164739") {
    _id
  }
}
      </pre>
    </td>
  </tr>  
</table>

