# bf-vue-admin

> Matieral design components for prophetech, which is based on ![vue.js 2.1+](https://vuejs.org/v2/guide/), ![muse-ui](http://www.muse-ui.org/#/install), etc.

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

## What we do

### Admin framework

* To register a new panel group, for example:

```javascript
/* src/components/panels/virtual/panels.js */
import {PanelGroup} from '@/router/base'

import instancePanel from './instances/panel'

export default new PanelGroup('Virtual', [
  instancePanel
], {
  icon: 'tv',
  slug: 'virtual'
})

/* src/router/index.js */
let dashboard = new Dashboard([
  Overview, Physical, Virtual, Setting
])
```

* To register a new panel, for example:

```javascript
/* src/components/panels/virtual/instances/panel.js */
import {Panel} from '@/router/base'

import InstanceIndex from './index.vue'
import InstanceDetail from './detail.vue'
import InstanceCreate from './create.vue'

export default new Panel('Instances', {
  name: 'virtual_instances',
  path: '/home/virtual/instances',
  component: InstanceIndex,
  children: [{
    path: '/home/virtual/instances/detail',
    component: InstanceDetail
  }, {
    path: '/home/virtual/instances/post/create',
    component: InstanceCreate
  }]
})
```

### Change theme

See follow picture:

![Change color](/source/change_color.jpeg)

### Table view

**Attention: Table view is not ready now, and detail documents will post later.**

To define a table view:

```javascript
<template>
  <div>
    <bf-table-view :show-select="true" :headers="headers"
                   :datas="datas" :show-actions="true"
                   :actions="actions" v-model="selected">
      <template slot="table-body-col-name" scope="that">
        <router-link :to="'/home/virtual/instances/' + that.data[that.header.slug]">{{that.data[that.header.slug]}}</router-link>
      </template>
    </bf-table-view>
  </div>

</template>

<script>

  export default {
    data () {
      let _this = this
      return {
        showSelect: true,
        selected: [],
        headers: [{
          name: 'Name',
          sort: true,
          slug: 'name'
        }, {
          name: 'Age',
          slug: 'age'
        }, {
          name: 'Color',
          slug: 'color'
        }],
        datas: [{
          name: 'Green Dream',
          age: '27',
          color: 'Grey'
        }, {
          name: 'Steven Curry',
          age: '30',
          color: 'Black'
        }, {
          name: 'Keven Durant',
          age: '28',
          color: 'Blue'
        }],
        showActions: true,
        actions: {
          more: {
            start: {
              icon: 'play_arrow',
              name: 'Start',
              all: 'single',
              handle () {
                console.log('do start')
              }
            },
            stop: {
              icon: 'pause',
              name: 'Stop',
              all: 'single',
              handle () {
                console.log('do start')
              }
            },
            update: {
              icon: 'update',
              name: 'Update',
              all: 'single',
              handle () {
                console.log('do start')
              }
            }
          },
          show: {
            create: {
              icon: 'add',
              name: 'Create',
              allow: 'all',
              type: 'primary',
              handle () {
                _this.$router.push({path: '/home/virtual/instances/post/create'})
              }
            },
            delete: {
              icon: 'delete',
              name: 'Delete',
              allow: 'single',
              type: 'secondary',
              handle () {
                console.log('do delete')
              }
            }
          },
          search: {
            bind: 'name'
          }
        }
      }
    }
  }
</script>
```

See actual effect:

![Table view](/source/table_view.jpeg)

### Form view

**Attention: Form view is not ready now, and detail documents will post later.**

To define a form view:

```javascript
<template>
  <bf-form-view :close-to="{name: 'physical_hosts'}"
                title="Create Host" :fields="fields" slug="host_create"
                :loading="false">
  </bf-form-view>
</template>

<script>

  export default {
    data () {
      return {
        fields: [{
          slug: 'hostname',
          label: 'Host Name',
          hint: 'Please input hostname'
        }, {
          slug: 'ip',
          label: 'Ip Addr',
          hint: 'Please input Ip address'
        }, {
          slug: 'password',
          type: 'password',
          label: 'Root password',
          hint: 'Please input root password'
        }, {
          slug: 'dep',
          type: 'select',
          label: 'Dependencies',
          hint: 'Please select dependencies hosts',
          options: [{
            val: '192.168.0.1',
            label: 'node-1'
          }, {
            val: '192.168.0.2',
            label: 'node-2'
          }]
        }]
      }
    },
    methods: {
    }
  }
</script>
```

See actual effect:

![Form view](/source/form_view.jpeg)

### Wizard view


**Attention: Wizard view is not ready now, and detail documents will post later.**

To define a wizard view:

```javascript
<template>
  <bf-wizard-view :close-to="{name: 'virtual_instances'}"
                  width="larger"
                  title="Create Server" :steps="steps" slug="instance_create"
                  :loading="false">
  </bf-wizard-view>
</template>

<script>

  export default {
    data () {
      return {
        steps: [{
          slug: 'basic',
          label: 'Basic Info',
          fields: [{
            slug: 'hostname1',
            label: 'Host Name',
            hint: 'Please input hostname'
          }, {
            slug: 'ip1',
            label: 'Ip Addr',
            hint: 'Please input Ip address'
          }, {
            slug: 'password1',
            type: 'password',
            label: 'Root password',
            hint: 'Please input root password'
          }, {
            slug: 'dep1',
            type: 'select',
            label: 'Dependencies',
            hint: 'Please select dependencies hosts',
            options: [{
              val: '192.168.0.1',
              label: 'node-1'
            }, {
              val: '192.168.0.2',
              label: 'node-2'
            }]
          }]
        }, {
          slug: 'second',
          label: 'Disk Info',
          fields: [{
            slug: 'hostname2',
            label: 'Host Name',
            hint: 'Please input hostname'
          }, {
            slug: 'ip2',
            label: 'Ip Addr',
            hint: 'Please input Ip address'
          }, {
            slug: 'password2',
            type: 'password',
            label: 'Root password',
            hint: 'Please input root password'
          }, {
            slug: 'dep2',
            type: 'select',
            label: 'Dependencies',
            hint: 'Please select dependencies hosts',
            options: [{
              val: '192.168.0.1',
              label: 'node-1'
            }, {
              val: '192.168.0.2',
              label: 'node-2'
            }]
          }]
        }, {
          slug: 'third',
          label: 'Network Info',
          fields: [{
            slug: 'hostname',
            label: 'Host Name',
            hint: 'Please input hostname'
          }, {
            slug: 'ip',
            label: 'Ip Addr',
            hint: 'Please input Ip address'
          }, {
            slug: 'password',
            type: 'password',
            label: 'Root password',
            hint: 'Please input root password'
          }, {
            slug: 'dep',
            type: 'select',
            label: 'Dependencies',
            hint: 'Please select dependencies hosts',
            options: [{
              val: '192.168.0.1',
              label: 'node-1'
            }, {
              val: '192.168.0.2',
              label: 'node-2'
            }]
          }]
        }]
      }
    },
    methods: {
    }
  }
</script>
```

See actual effect:

![Wizard view](/source/wizard_view.jpeg)
