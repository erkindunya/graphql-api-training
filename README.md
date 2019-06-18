# Relay Cursor Connections

This exercise is part of the [React GraphQL Academy](http://reactgraphql.academy) learning material. The goal of this exercise is to help you understand how Relay Cursor Connections work.

## Learning objectives

- Understand Relay Cursor Connections
- Learn how and when to use GraphQL interfaces, unions, and fragments

## To get started

### Step 1

If you haven't already set up your project, head here and follow the instructions https://github.com/reactgraphqlacademy/graphql-api-training/blob/master/README.md

### Step 2

```console
git checkout relay
```

### Step 3

```console
yarn
```

## Exercise

- 1. Since we are going to share the same field id in different types, we are going to define an interface for it. [Official GraphQL documenation about interfaces](https://graphql.org/learn/schema/#interfaces). Tasks:
  - [ ] 1.1. Create in interface called INode with a field ID that can't be null.
  - [ ] 1.2. Character should implement the INode interface
  - [ ] 1.3. Episode should implement the INode interface. Hint, the ID type in Episode is not correct so you need to update it to comply with the interface
- 2. In order to be Relay compliant the GraphQL server needs to be able to retrive any node in the system by id.
  - [ ] 2.1. Implement a [union](https://graphql.org/learn/schema/#union-types) called `Node` in the schema made of `Episode` and `Character`
  - [ ] 2.2. Finalize the `getObjectById` function. This function receives the name of the type and id, and maps that type with the function that retrieves the data by id.
  - [ ] 2.3. Implement a field called `node` in the `Query` type that given an ID! returns the actual object.
  - [ ] 2.4. Implement the resolver for the `node` field. Use the `getObjectById` you've implemented and the `fromGlobalId` function imported from [graphql-relay](https://github.com/graphql/graphql-relay-js/blob/master/src/node/node.js#L104)
  - [ ] 2.5. The `Character` type should override the default resolver for the field `id` and use `toGlobalId` to return a global id for that type.
  - [ ] 2.6. Add a resolver for the `Node` type that implements the `__resolveType(obj){}` function. You can check the Apollo [documentation about unions](https://www.apollographql.com/docs/apollo-server/features/unions-interfaces/#union-type). To infer the types in this case you can consider that if the object as a key called `episode` then it's a `Character` type. The opposite is also true, if the object as a field called `character` then it's an `Episode` type.
- 3. Now you should be able to find any node by id.
  - [ ] 3.1. Use the `query characters` in Playground and ask for the id. You should see that it's not an number anymore. It's a global id.
  - [ ] 3.2. Use any of the global Character ids to query a node by id. Hint, you need to use a [fragment](https://graphql.org/learn/queries/#inline-fragments)
- 4. Let's use the CharacterConnection.
  - [ ] 4.1. Add a field to the `Query` type called `charactersConnection`.
  - [ ] 4.2. Implement a resolver for the charactersConnection. Do you think you can map all the required fields in CharacterConnection using the [response from the API](https://rickandmortyapi.com/api/character/)? Hint: If you try and you can't then try to use the `mockedCharacters` data and `connectionFromArray` function imported at the top as a "workaround".

### Bonus

- Create the field connectionCharacters in the Episode to return a CharactersConnection

## Articles and links

- http://graphql.org/learn/
- http://graphql.org/learn/thinking-in-graphs/
- https://dev-blog.apollodata.com/graphql-vs-rest-5d425123e34b
- https://dev-blog.apollodata.com/graphql-explained-5844742f195e
- https://facebook.github.io/relay/docs/thinking-in-graphql.html
- https://dev-blog.apollodata.com/the-anatomy-of-a-graphql-query-6dffa9e9e747
- https://github.com/apollographql/apollo-server
- https://www.youtube.com/watch?v=PHabPhgRUuU
- https://facebook.github.io/relay/graphql/connections.htm
- https://dev-blog.apollodata.com/introducing-launchpad-the-graphql-server-demo-platform-cc4e7481fcba
- https://dev-blog.apollodata.com/
- http://dev.apollodata.com
- https://astexplorer.net/

## License

This material is available for private, non-commercial use under the [GPL version 3](http://www.gnu.org/licenses/gpl-3.0-standalone.html).
