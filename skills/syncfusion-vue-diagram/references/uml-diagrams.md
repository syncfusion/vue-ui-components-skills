# UML Diagrams in Syncfusion Vue Diagram

## Table of Contents
- [Overview](#overview)
- [UML Setup](#uml-setup)
- [Class Diagrams](#class-diagrams)
- [Classifiers](#classifiers)
- [UML Relationships](#uml-relationships)
- [Sequence Diagrams](#sequence-diagrams)
- [Lifelines](#lifelines)
- [Messages](#messages)

## Overview

UML (Unified Modeling Language) provides diagrams for software design and architecture. Syncfusion supports UML class diagrams, sequence diagrams, and various relationship types for technical documentation.

## UML Setup


### Basic Usage

```vue
<template>
  <ejs-diagram id="diagram" :width="width" :height="height" :nodes="nodes" />
</template>

<script setup>
import { DiagramComponent } from '@syncfusion/ej2-vue-diagrams';
import { ref } from 'vue';

const width = '100%';
const height = '590px';
const nodes = ref([]); // Add UML nodes as shown below
</script>
<style>
@import "../node_modules/@syncfusion/ej2-vue-diagrams/styles/material.css";
</style>
```

## Class Diagrams


### Class Classifier

```javascript
const classNode = {
  id: 'class1',
  width: 200,
  height: 150,
  offsetX: 250,
  offsetY: 250,
  shape: {
    type: 'UmlClassifier',
    classShape: {
      name: 'ClassName',
      attributes: [
        { name: 'property1', type: 'string' },
        { name: 'property2', type: 'number' }
      ],
      methods: [
        { name: 'method1', type: 'void' },
        { name: 'method2', type: 'boolean' }
      ]
    },
    classifier: 'Class'
  }
};
```


### Interface Classifier

```javascript
const interfaceNode = {
  id: 'interface1',
  width: 200,
  height: 120,
  shape: {
    type: 'UmlClassifier',
    interfaceShape: {
      name: 'IExample',
      attributes: [],
      methods: [
        { name: 'doSomething', type: 'void' }
      ]
    },
    classifier: 'Interface'
  }
};
```


### Enumeration Classifier

```javascript
const enumNode = {
  id: 'enum1',
  width: 150,
  height: 120,
  shape: {
    type: 'UmlClassifier',
    enumerationShape: {
      name: 'Status',
      members: [
        { name: 'Active' },
        { name: 'Inactive' },
        { name: 'Pending' }
      ]
    },
    classifier: 'Enumeration'
  }
};
```


### Abstract Class

```javascript
const abstractClass = {
  id: 'abstractClass1',
  width: 200,
  height: 150,
  shape: {
    type: 'UmlClassifier',
    classShape: {
      name: 'BaseClass',
      attributes: [{ name: 'abstractProperty', type: 'T' }],
      methods: [
        { name: 'abstractMethod', type: 'void' },
        { name: 'concreteMethod', type: 'boolean' }
      ]
    },
    classifier: 'Abstract'
  }
};
```


### Visibility Modifiers

```javascript
const classWithModifiers = {
  shape: {
    type: 'UmlClassifier',
    classShape: {
      attributes: [
        { name: 'publicProperty', type: 'string', scope: 'public' },
        { name: 'protectedProperty', type: 'number', scope: 'protected' },
        { name: 'privateProperty', type: 'boolean', scope: 'private' },
        { name: 'packageProperty', type: 'object', scope: 'package' }
      ],
      methods: [
        { name: 'publicMethod', type: 'void', scope: 'public' },
        { name: 'privateMethod', type: 'string', scope: 'private' }
      ]
    },
    classifier: 'Class'
  }
};
```

## Classifiers

All classifiers extend from base class definition:


### Classifier Properties

```javascript
const classifier = {
  shape: {
    type: 'UmlClassifier',
    classShape: {
      name: 'ClassName',
      attributes: [
        { name: 'propertyName', type: 'PropertyType' }
      ],
      methods: [
        { name: 'methodName', type: 'ReturnType', parameters: [{ name: 'param', type: 'ParamType' }] }
      ],
      separator: true
    },
    classifier: 'Class'
  }
};
```

## UML Relationships


### Association

Generic relationship between classes:

```javascript
const association = {
  id: 'assoc1',
  sourceID: 'class1',
  targetID: 'class2',
  type: 'Straight',
  shape: {
    type: 'UmlClassifier',
    relationship: 'Association',
    association: 'BiDirectional' // or 'Directional'
  }
};
```


### Inheritance (Generalization)

```javascript
const inheritance = {
  id: 'inherit1',
  sourceID: 'childClass',
  targetID: 'parentClass',
  type: 'Straight',
  shape: {
    type: 'UmlClassifier',
    relationship: 'Inheritance'
  }
};
```


### Realization (Interface Implementation)

```javascript
const realization = {
  id: 'realize1',
  sourceID: 'implementingClass',
  targetID: 'interfaceClass',
  type: 'Straight',
  shape: {
    type: 'UmlClassifier',
    relationship: 'Realization'
  },
  style: { strokeDashArray: '5,5' }
};
```


### Dependency

Weaker relationship indicating usage:

```javascript
const dependency = {
  id: 'depend1',
  sourceID: 'dependentClass',
  targetID: 'dependencyClass',
  type: 'Straight',
  shape: {
    type: 'UmlClassifier',
    relationship: 'Dependency'
  },
  style: { strokeDashArray: '5,5' }
};
```


### Aggregation

One class contains instances of another:

```javascript
const aggregation = {
  id: 'aggr1',
  sourceID: 'containerClass',
  targetID: 'containedClass',
  type: 'Straight',
  shape: {
    type: 'UmlClassifier',
    relationship: 'Aggregation'
  }
};
```


### Composition

Strong ownership relationship:

```javascript
const composition = {
  id: 'comp1',
  sourceID: 'ownerClass',
  targetID: 'ownedClass',
  type: 'Straight',
  shape: {
    type: 'UmlClassifier',
    relationship: 'Composition'
  }
};
```


## UML Sequence Diagrams (Vue 3)

UML Sequence diagrams use a model-based approach. Use the `model` property of the diagram instance.

### Participants and Messages

```vue
<template>
  <ejs-diagram ref="diagramRef" id="diagram" width="100%" height="600px" />
</template>
<script setup>
import { ref, onMounted } from 'vue';
import { DiagramComponent } from '@syncfusion/ej2-vue-diagrams';
import { UmlSequenceMessageType, SnapConstraints } from '@syncfusion/ej2-diagrams';

const model = {
  participants: [
    { id: 'User', content: 'User', isActor: true },
    { id: 'System', content: 'System', isActor: false, showDestructionMarker: true }
  ],
  messages: [
    { id: 'MSG1', content: 'Login Request', fromParticipantID: 'User', toParticipantID: 'System', type: UmlSequenceMessageType.Synchronous },
    { id: 'MSG2', content: 'Login Response', fromParticipantID: 'System', toParticipantID: 'User', type: UmlSequenceMessageType.Reply }
  ]
};
const snapSettings = { constraints: SnapConstraints.None };
const diagramRef = ref(null);
onMounted(() => {
  const diagramInstance = diagramRef.value.ej2Instances;
  diagramInstance.model = model;
  diagramInstance.updateFromModel();
});
</script>
<style scoped>
@import "../node_modules/@syncfusion/ej2-vue-diagrams/styles/material.css";
@import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
</style>
```

### Participant Lifeline

```javascript
const participantLifeline = {
  id: 'system1',
  width: 100,
  height: 300,
  offsetX: 300,
  offsetY: 200,
  shape: {
    type: 'UmlSequence',
    sequence: {
      name: 'System',
      lifeline: {
        name: 'participant'
      }
    }
  }
};
```

## Messages

### Asynchronous Message

```javascript
const asyncMessage = {
  id: 'msg2',
  sourceID: 'system1',
  targetID: 'actor1',
  shape: {
    type: 'UmlSequence',
    sequence: {
      message: {
        type: 'Asynchronous'         // Open arrow
      }
    }
  },
  annotations: [{ content: 'response()' }]
};
```

### Reply Message

```javascript
const replyMessage = {
  id: 'msg3',
  sourceID: 'system1',
  targetID: 'actor1',
  shape: {
    type: 'UmlSequence',
    sequence: {
      message: {
        type: 'Reply'                // Dashed line
      }
    }
  },
  style: { strokeDashArray: '5,5' },
  annotations: [{ content: 'return' }]
};
```

### Create Message

```javascript
const createMessage = {
  id: 'msg4',
  sourceID: 'actor1',
  targetID: 'newObject',
  shape: {
    type: 'UmlSequence',
    sequence: {
      message: {
        type: 'Create'
      }
    }
  }
};
```

### Delete Message

```javascript
const deleteMessage = {
  id: 'msg5',
  sourceID: 'actor1',
  targetID: 'destroyedObject',
  shape: {
    type: 'UmlSequence',
    sequence: {
      message: {
        type: 'Delete'
      }
    }
  }
};
```

### Lost/Found Message

```javascript
const lostMessage = {
  id: 'msg6',
  sourceID: 'actor1',
  targetID: 'endpoint',
  shape: {
    type: 'UmlSequence',
    sequence: {
      message: {
        type: 'Lost'
      }
    }
  }
};
```

UML diagrams enable technical teams to communicate software design, architecture, and object relationships clearly and consistently.
