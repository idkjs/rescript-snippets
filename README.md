# Rescript/ReasonML tools

by [AlainArmand](https://vnovick.com). Twitter: [@VladimirNovick](https://twitter.com/_idkjs)

This extension contains code snippets for [Rescript](https://rescript-lang.org/) and it's usage with GraphQL along with some useful snippets for writing external bindings, requiring JavaScript etc. It is WIP and will contain various additional tools in the nearest future. List of features:


- Snippets for
  - Rescript
    - core syntax
    - Bucklescript, Belt
  - Reascript With React
  - reason-apollo-client


## Installation

In order to install an extension you need to launch the Command Pallete (Ctrl + Shift + P or Cmd + Shift + P) and type Extensions. There you have either the option to show the already installed snippets or install new ones.

Supported languages (file extensions)
Reason (.res, resi)

## Usage

After installing extension you can type snippets starting with `res` prefix and will get auto completion for common use cases for both Reason and ReasonReact. Reason GraphQL snippets will be prefixed with `resgql`

### Snippets

Every snippet will have $1, $2 and so on placeholders. when using snippet you can navigate from one placeholder to the other using Tab


#### FFI - include your javascript

- `resreq` - require external javascript package and assing a let binding to it.

```rescript
@bs.val external require: string => string = "",
let $1 = require("$2");
```

- `resbsglobal` - Bucklescript global value binding

```rescript
@bs.val external $bindingToBeCalledInReason: $typeSignature = "$functionNameOnGlobalScope"
```


- `resbsnullundefined` - Null or Undefined type
```rescript
Js.Nullable.t<string>
```



#### ReasonReact

- `resstr` - add `React.string` pipe to string in JSX component

```rescript
{$1 ->React.string }
```

- `rescmp` - Write basic ReasonML component with JSX 3 syntax

```rescript
@react.component,
let make = ($1) => {
  $2
}
```

- `resdomrender` - ReactDom Render

```rescript
ReactDOMRe.renderToElementWithId(
  <$ComponentName $prop />,
  "$element",
);
```



- `resred` - add `useReducer` hook in ReasonReact

```rescript
@react.component
let make = () => {
  let (state, dispatch) = React.useReducer((state, action)=>
    switch (action) {
      | $1 => { $2 }
    } , { $3 }

);
```

- `reseff1` - ReasonReact useEffect1

```rescript
React.useEffect1(
    () => {
      $returnToUnsubscribeOrNone
    },
  [$dependency],
);
```

- `resstate` - React.useState hook

```rescript
let ($1, set$1) = React.useState(() => $2);
```

- `reseff0` - React.useEffect hook

```rescript
React.useEffect0(() => {
  $sideeffect
});
```

- `reseff0` - React.useEffect hook

```rescript
React.useEffect0(() => {

});
```

- `resjscmpdefault` - Bring React component from Js

```rescript
@bs.module "$1"@react.component
external make: ($2: $3) => React.element = "default";
```

- `reseventtarget` - get form `event.target.value`

```rescript
e => e->ReactEvent.Form.target##value |> $1
```

- `resstyle` - write inline style

```rescript
let $1 = ReactDOMRe.Style.make($2);
```

#### GraphQL

#### Reason Apollo Client

- `resgqlhttp` - ReasonApollo http link

```rescript
  let httpLink = ApolloClient.Link.HttpLink.make(~uri="$1", ());
```


- `resgqlapolloc`

```rescript
let inMemoryCache = ApolloClient.Cache.InMemoryCache.make();

ApolloClient.make(
  ~link,
  ~cache=inMemoryCache,
  (),
);
```

- `resgqlsplit`

```rescript
let link = ApolloClient.Link.split(operation => {
  let operationDefition = ApolloUtilities.getMainDefinition(operation.["query"])
  operationDefition.["kind"] == "OperationDefinition" &&
    operationDefition.["operation"] == "subscription"
}, webSocketLink, httpLink)
```

- `resgqlws`

```rescript
  let webSocketLink = {
  open ApolloClient.Link.WebSocketLink
      make(
            ~uri="$1"
            ~reconnect=true,
          (),
        ),
    (),
  )
}
```


- `resgql` - gql for your queries, mutations, subscription

```rescript
module $1 = %graphql
  `
     $2
  `
;
```

- `resgqlrp` Render prop snippet

```rescript
  <$1>
    ...{($2) => {
        $3
      }
    }
  </$1>
```

- `resgqlm` mutation function

```rescript
mutation(~variables=$1##variables,()) |> ignore;
```

# Release Notes

## 0.0.1

Initial release of Rescript/React and GraphQL snippets

---
