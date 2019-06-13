# FaunaDB: Sample DB



#### Table of Contents
* [Schema](#schema)
* [Query Reference](#query-reference)
  * [Warehouse](#warehouse)
  * [Product](#product)

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
      "name": "East"
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
      name: "East"
      address: {
        street: "1 Corry Plaz"
        city: "Stockton"
        state: "CA"
        zipCode: "95205"
      }
    }
  ){
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
  <tr>
    <td valign="top"><b>Read all<br>Warehouses</b></td>
    <td valign="top">
     <pre>
Map(
  Paginate(Match(Index("allWarehouses"))),
  Lambda("nextRef", Get(Var("nextRef")))
);
      </pre>
    </td>
    <td valign="top">
      <pre>
query {
  allWarehouses {
    data {
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
}
      </pre>
    </td>
  </tr>
</table>

### Product

<table>
  <tr>
    <th>Operation</th>
    <th>FQL</th>
    <th>GraphQL</th>
  </tr>
  <tr>
    <td valign="top"><b>Create a<br>Product</b></td>
    <td valign="top">
      <pre>
Create(
  Class("Product"), {
    data: {
      "name": "Cup",
      "description": "Translucent 9 Oz",
      "price": 6.90,
      "quantity": 100,
      "warehouseId": Ref(Class("Warehouses"), "1549398205020000"),
      "backorderLimit": 10,
      "backordered": false
    }
  }
);
	  </pre>
    </td>
    <td valign="top">
      <pre>
mutation {
  createProduct(data: {
    name: "Cup",
    description: "Translucent 9 Oz",
    price: 6.90,
    quantity: 100,
    warehouse: {
      connect: "1549398205020000" 
    },
    backorderLimit: 10,
    backordered: false
}){
    _id
  } 
}
		</pre>
    </td>
  </tr>
  <tr>
    <td valign="top"><b>Read a<br>Product</b></td>
    <td valign="top">
      <pre>
Get(Ref(Class("Product"), "220510522473185799"));
      </pre>
    </td>
    <td valign="top">
      <pre>
query {
  findProductByID(id: "220510522473185799") {
    _id
    name
  	description
  	price
	quantity
	backorderLimit
  	backordered
  }
}
      </pre>
    </td>
  </tr>
  <tr>
    <td valign="top"><b>Update a<br>Product</b></td>
    <td valign="top">
     <pre>
Update(
  Ref(Class("Product"), "220510522473185799"), {
    data: {
      "name": "Cup",
      "description": "Translucent 9 Oz",
      "price": 7.90,
      "quantity": 100,
      "warehouseId": Ref(Class("Warehouses"), "1549398205020000"),
      "backorderLimit": 10,
      "backordered": false
    }
  }
);
      </pre>
    </td>
    <td valign="top">
      <pre>
mutation {
  updateProduct(
    id: "220510522473185799"
    data: {
      name: "Cup",
      description: "Translucent 9 Oz",
      price: 7.90,
      quantity: 100,
      backorderLimit: 10,
      backordered: false
    }
  ){
    _id
  }
}      </pre>
    </td>
  </tr>
<tr>
    <td valign="top"><b>Delete a<br>Product</b></td>
    <td valign="top">
     <pre>
Delete(Ref(Class("Product"), "220510522473185799"))
      </pre>
    </td>
    <td valign="top">
      <pre>
mutation {
  deleteProduct(id: "220510522473185799") {
    _id
  }
}
      </pre>
    </td>
  </tr>
    <tr>
    <td valign="top"><b>Read all<br>Products</b></td>
    <td valign="top">
     <pre>
Map(
  Paginate(Match(Index("allProducts"))),
  Lambda("nextRef", Get(Var("nextRef")))
);
      </pre>
    </td>
    <td valign="top">
      <pre>
query {
  allWarehouses {
    data {
      name
      address {
        street
        city
        state
        zipCode
      }
    }
  }
}
      </pre>
    </td>
  </tr>
</table>

