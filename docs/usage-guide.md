# Usage Guide

## Overview

This guide provides instructions on how to use Metaclass to define and work with digital existence through constraint geometry.

## Core Concepts

Before diving into usage, familiarize yourself with these core concepts:

- **Axis**: Foundational dimensions of existence (e.g., Continuity, Rigidity, Causality)
- **Constraint Bundle**: A set of constraints that define a stable region in the constraint space
- **Stability**: A valid existence must be stable (constraints must converge)
- **Projection**: Mapping from constraint space to operational domains

## Defining a Constraint Bundle

To define a new constraint bundle, create a `.bundle.json` file in the `bundles` directory:

```json
{
  "name": "liquid",
  "version": "1.0.0",
  "axes": [
    {
      "name": "continuity",
      "range": [0.8, 1.0]
    },
    {
      "name": "rigidity",
      "range": [0.0, 0.2]
    },
    {
      "name": "flowability",
      "range": [0.8, 1.0]
    }
  ],
  "stability": {
    "method": "entropy",
    "threshold": 0.9
  }
}
```

## Using Projections

Projections map constraint spaces to operational domains. Here's how to define a physics projection:

```typescript
// physics.projection.ts
import { Projection } from '@metaclass/core';

export const PhysicsProjection: Projection = {
  name: "physics",
  version: "1.0.0",
  map: (constraints) => {
    // Map constraints to physics parameters
    return {
      density: constraints.find(c => c.axis === "density")?.value || 1.0,
      viscosity: constraints.find(c => c.axis === "viscosity")?.value || 0.0,
      elasticity: constraints.find(c => c.axis === "elasticity")?.value || 0.0
    };
  }
};
```

## Creating an Instance

To create an instance of a constraint bundle:

```typescript
import { MetaclassSystem } from '@metaclass/core';
import { LiquidBundle } from './bundles/liquid.bundle.json';

// Initialize the system
const system = new MetaclassSystem();

// Create an instance
const water = system.createInstance(LiquidBundle, {
  temperature: 20,
  pressure: 1
});

// Check stability
const isStable = system.checkStability(water);
console.log(`Water instance is stable: ${isStable}`);

// Project to physics domain
const physicsParams = system.project(water, "physics");
console.log('Physics parameters:', physicsParams);
```

## Working with Rooms

Rooms are different perspectives on the same constraint bundle. To define a room:

```json
{
  "name": "cartesian",
  "bundle": "liquid",
  "parameters": {
    "position": [0, 0, 0],
    "velocity": [0, 0, 0],
    "acceleration": [0, 0, 0]
  }
}
```

## Evolution and Transformation

Metaclass allows entities to evolve over time. Here's how to simulate evolution:

```typescript
// Simulate temperature change
const heatedWater = system.evolve(water, {
  temperature: 100
});

// Check if it's still water or has become steam
const isStillWater = system.matchesBundle(heatedWater, LiquidBundle);
console.log(`Still water after heating: ${isStillWater}`);
```

## Best Practices

1. **Start with Core Axes**: Begin by defining constraints on the core axes (Continuity, Rigidity, Causality).

2. **Use Stability Thresholds**: Always set appropriate stability thresholds to ensure valid existences.

3. **Version Your Bundles**: Maintain version control for your constraint bundles to track changes.

4. **Test Projections**: Verify that projections correctly map constraints to their respective domains.

5. **Document Edge Cases**: Document how your constraint bundles behave at the boundaries of their constraint ranges.

## Examples

For more examples, see the `instances` directory in the repository, which contains sample constraint bundles and their usage.
