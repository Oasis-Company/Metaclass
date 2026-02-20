# API Reference

## Core Classes

### MetaclassSystem

The main entry point for the Metaclass system.

#### Constructor

```typescript
new MetaclassSystem(config?: MetaclassConfig)
```

**Parameters:**
- `config`: Optional configuration object

#### Methods

##### `createInstance(bundle: ConstraintBundle, initialState?: Record<string, any>): MetaclassInstance`

Creates a new instance of a constraint bundle.

**Parameters:**
- `bundle`: The constraint bundle to instantiate
- `initialState`: Optional initial state values

**Returns:**
- A new `MetaclassInstance` object

##### `checkStability(instance: MetaclassInstance): boolean`

Checks if an instance is stable.

**Parameters:**
- `instance`: The instance to check

**Returns:**
- `true` if the instance is stable, `false` otherwise

##### `project(instance: MetaclassInstance, projection: string): any`

Projects an instance to a specific domain.

**Parameters:**
- `instance`: The instance to project
- `projection`: The name of the projection

**Returns:**
- The projected values

##### `evolve(instance: MetaclassInstance, changes: Record<string, any>): MetaclassInstance`

Evolves an instance with the given changes.

**Parameters:**
- `instance`: The instance to evolve
- `changes`: The changes to apply

**Returns:**
- A new evolved `MetaclassInstance`

##### `matchesBundle(instance: MetaclassInstance, bundle: ConstraintBundle): boolean`

Checks if an instance matches a constraint bundle.

**Parameters:**
- `instance`: The instance to check
- `bundle`: The constraint bundle to match against

**Returns:**
- `true` if the instance matches the bundle, `false` otherwise

### ConstraintBundle

Defines a set of constraints that form a stable region in the constraint space.

#### Properties

- `name`: string - The name of the bundle
- `version`: string - The version of the bundle
- `axes`: Array<AxisConstraint> - The axis constraints
- `stability`: StabilityConfig - The stability configuration

### MetaclassInstance

Represents an instance of a constraint bundle.

#### Properties

- `id`: string - Unique identifier
- `bundle`: ConstraintBundle - The bundle this instance is based on
- `state`: Record<string, any> - Current state values
- `createdAt`: Date - Creation timestamp
- `updatedAt`: Date - Last update timestamp

#### Methods

##### `getState(): Record<string, any>`

Gets the current state of the instance.

**Returns:**
- The current state

##### `setState(changes: Record<string, any>): void`

Sets the state of the instance.

**Parameters:**
- `changes`: The changes to apply

## Projections

### Projection Interface

```typescript
interface Projection {
  name: string;
  version: string;
  map: (constraints: Array<Constraint>) => any;
}
```

**Properties:**
- `name`: The name of the projection
- `version`: The version of the projection
- `map`: A function that maps constraints to the target domain

## Axes

### Axis Interface

```typescript
interface Axis {
  name: string;
  domain: Domain;
  metric?: Metric;
  continuous?: boolean;
  periodic?: boolean;
}
```

**Properties:**
- `name`: The name of the axis
- `domain`: The valid domain for values
- `metric`: Optional metric for measuring distance
- `continuous`: Whether the axis is continuous
- `periodic`: Whether the axis is periodic

## Stability

### StabilityConfig Interface

```typescript
interface StabilityConfig {
  method: 'convergence' | 'entropy' | 'energy';
  threshold: number;
}
```

**Properties:**
- `method`: The stability method to use
- `threshold`: The threshold for stability

## Registry

### AxisRegistry

Manages the registry of available axes.

#### Methods

##### `register(axis: Axis): void`

Registers a new axis.

**Parameters:**
- `axis`: The axis to register

##### `get(name: string): Axis | undefined`

Gets an axis by name.

**Parameters:**
- `name`: The name of the axis

**Returns:**
- The axis if found, `undefined` otherwise

##### `list(): Array<Axis>`

Lists all registered axes.

**Returns:**
- An array of all registered axes

## Error Handling

### MetaclassError

Base error class for Metaclass errors.

#### Properties

- `message`: string - Error message
- `code`: string - Error code
- `details`: any - Additional error details

### Common Error Codes

- `INVALID_BUNDLE`: Invalid constraint bundle
- `INSTANCE_UNSTABLE`: Instance is not stable
- `PROJECTION_NOT_FOUND`: Projection not found
- `AXIS_NOT_REGISTERED`: Axis not registered
- `CONSTRAINT_VIOLATION`: Constraint violation

## Events

### MetaclassSystem Events

- `instance.created`: Emitted when a new instance is created
- `instance.evolved`: Emitted when an instance is evolved
- `instance.stabilityChanged`: Emitted when an instance's stability changes
- `bundle.registered`: Emitted when a new bundle is registered
- `projection.registered`: Emitted when a new projection is registered
