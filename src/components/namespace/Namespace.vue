// Copyright (C) 2019 Contributors as noted in the AUTHORS file
// 
// This file is part of nem2-wallet-browserextension.
// 
// nem2-wallet-browserextension is free software: you can redistribute it and/or modify
// it under the terms of the GNU General Public License as published by
// the Free Software Foundation, either version 3 of the License, or
// (at your option) any later version.
// 
// nem2-wallet-browserextension is distributed in the hope that it will be useful,
// but WITHOUT ANY WARRANTY; without even the implied warranty of
// MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
// GNU General Public License for more details.
// 
// You should have received a copy of the GNU General Public License
// along with nem2-wallet-browserextension.  If not, see <http://www.gnu.org/licenses/>.

<template>
  <v-layout
    column
    xs12
  >
    <v-layout
      row
      mb-4
    >
      <v-layout
        row
        fill-height
        justify-start
        pl-3
        xs3
      >
        <h5 class="headline pt-3">
          Namespace
        </h5>
      </v-layout>
      <v-layout
        row
        fill-height
        justify-end
        xs9
      >
        <v-btn
          color="primary mx-0"
          @click="reloadList"
        >
          Reload List
        </v-btn>
        <v-btn
          class="ml-3"
          color="primary mx-0"
          @click="registerNamespace = !registerNamespace"
        >
          Register Namespace
        </v-btn>
      </v-layout>
    </v-layout>

    <Errors :shared-state="sharedState" />
    <NamespaceRegistration
      v-if="registerNamespace"
      @closeComponent="registerNamespace = false"
    />
    <div
      v-if="sharedState.wallets.length > 0
        && sharedState.activeWallet
        && !sharedState.error"
    >
      <NamespaceList
        class="my-2"
      />
    </div>
  </v-layout>
</template>
<script>
import StateRepository from '../../infrastructure/StateRepository';
import Errors from '../Errors.vue';
import NamespaceRegistration from './NamespaceRegistration.vue';
import NamespaceList from './NamespaceList.vue';

export default {
  components: {
    Errors,
    NamespaceRegistration,
    NamespaceList,
  },
  data() {
    return {
      sharedState: StateRepository.state,
      registerNamespace: false,
    };
  },
  methods: {
    reloadList() {
      StateRepository.loadNamespaces();
    },
  },
};
</script>
<style scoped>
</style>
