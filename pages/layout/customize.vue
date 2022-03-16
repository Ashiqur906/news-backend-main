<template>
<v-container>
  <v-row>
    <!-- Layout Start -->
    <v-col cols="12" md="8" sm="6">
      <!-- Row One Header Part -->
      <v-row>
        <v-col cols="12" sm="12" elevation="2">
          <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
            <div align="right">
              <nuxt-link :to="{ name: 'layout-update-id', params: { id: 1 }}">
                <edit-button />
              </nuxt-link>
            </div>
            <div class="text-center justify-center ">
              {{widget_setting['header']?widget_setting['header']['title']:''}}
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[0]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[0]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[0]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[0]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </div>
          </v-card>
        </v-col>
      </v-row>
      <!-- Row One Marquee Part -->
      <v-row>
        <v-col cols="12" sm="12" elevation="2">
          <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
            <div align="right">
              <nuxt-link :to="{ name: 'layout-update-id', params: { id: 2 }}">
                <edit-button />
              </nuxt-link>
            </div>
            <div class="text-center justify-center ">
              {{widget_setting['marquee']?widget_setting['marquee']['title']:''}}
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[1]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[1]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[1]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[1]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </div>
          </v-card>
        </v-col>
      </v-row>
      <!-- Row Two Heading News -->
      <v-card class="mx-auto ma-5" outlined rounded="lg">
        <v-row>
          <!-- Left Section   -->
          <v-col cols="12" sm="3" elevation="2">
            <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
              <div class="text-right">
                <nuxt-link :to="{ name: 'layout-update-id', params: { id: 3 }}">
                  <edit-button />
                </nuxt-link>
              </div>
              <div class="text-center">
                Widget Three (Left Section)
              </div>
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[2]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[2]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[2]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[2]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </v-card>
          </v-col>
          <!-- Middle Section   -->
          <v-col cols="12" sm="5" elevation="2">
            <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
              <div class="text-right">
                <nuxt-link :to="{ name: 'layout-update-id', params: { id: 4 }}">
                  <edit-button />
                </nuxt-link>
              </div>
              <div class="text-center">
                Widget Four (Main Section)
              </div>
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[3]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[3]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[3]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[3]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </v-card>
          </v-col>
          <!-- Right Section   -->
          <v-col cols="12" sm="4" elevation="2">
            <v-row>
              <!-- Live Tv  -->
              <v-col cols="12">
                <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
                  <div class="text-right">
                    <nuxt-link :to="{ name: 'layout-update-id', params: { id: 5 }}">
                      <edit-button />
                    </nuxt-link>
                  </div>
                  <div class="text-center">
                    Widget Five (Live Tv)
                  </div>
                  <div class="text-center ma-2 col-md-">
                    <template>
                      <v-simple-table dense>
                        <thead>
                          <tr>
                            <th class="text-left">
                              Ttile
                            </th>
                            <th class="text-left">
                              Data
                            </th>
                          </tr>
                        </thead>
                        <tbody class="text-left">
                          <tr>
                            <td>Data Type</td>
                            <td>{{ widgets[4]['data_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Widget Type</td>
                            <td>{{ widgets[4]['widget_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Data Limit</td>
                            <td>{{ widgets[4]['data_limit'] }}</td>
                          </tr>
                          <tr>
                            <td>Status</td>
                            <td>
                              <v-chip v-if="widgets[4]['widget_status'] == 1" color="success" text-color="white" bold>
                                Active
                              </v-chip>
                              <v-chip v-else color="red" text-color="white">
                                Inactive
                              </v-chip>
                            </td>
                          </tr>
                        </tbody>
                      </v-simple-table>
                    </template>
                  </div>
                </v-card>
              </v-col>
              <!-- News  -->
              <v-col cols="12">
                <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
                  <div class="text-right">
                    <nuxt-link :to="{ name: 'layout-update-id', params: { id: 6 }}">
                      <edit-button />
                    </nuxt-link>
                  </div>
                  <div class="text-center">
                    Widget Six (News)
                  </div>
                  <div class="text-center ma-2 col-md-">
                    <template>
                      <v-simple-table dense>
                        <thead>
                          <tr>
                            <th class="text-left">
                              Ttile
                            </th>
                            <th class="text-left">
                              Data
                            </th>
                          </tr>
                        </thead>
                        <tbody class="text-left">
                          <tr>
                            <td>Data Type</td>
                            <td>{{ widgets[5]['data_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Widget Type</td>
                            <td>{{ widgets[5]['widget_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Data Limit</td>
                            <td>{{ widgets[5]['data_limit'] }}</td>
                          </tr>
                          <tr>
                            <td>Status</td>
                            <td>
                              <v-chip v-if="widgets[5]['widget_status'] == 1" color="success" text-color="white" bold>
                                Active
                              </v-chip>
                              <v-chip v-else color="red" text-color="white">
                                Inactive
                              </v-chip>
                            </td>
                          </tr>
                        </tbody>
                      </v-simple-table>
                    </template>
                  </div>
                </v-card>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
      </v-card>
      <!-- Row Three -->
      <v-card class="mx-auto ma-5" outlined rounded="lg">
        <v-row>
          <!-- Widget Seven -->
          <v-col cols="12" sm="5" elevation="2">
            <v-card class="mx-auto" outlined rounded="lg" min-height="250px">
              <div class="text-right">
                <nuxt-link :to="{ name: 'layout-update-id', params: { id: 7 }}">
                  <edit-button />
                </nuxt-link>
              </div>
              <div class="text-center">
                {{widget_setting['post']?widget_setting['post']['title']:''}}
              </div>
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[6]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[6]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[6]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[6]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </v-card>
          </v-col>
          <!-- Widget Eight -->
          <v-col cols="12" sm="4" elevation="2">
            <v-card class="mx-auto" outlined rounded="lg" min-height="250px">
              <div class="text-right">
                <nuxt-link :to="{ name: 'layout-update-id', params: { id: 8 }}">
                  <edit-button />
                </nuxt-link>
              </div>
              <div class="text-center">
                {{widget_setting['post']?widget_setting['post']['title']:''}}
              </div>
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[7]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[7]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[7]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[7]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </v-card>
          </v-col>
          <!-- Widget Nine -->
          <v-col cols="12" sm="3" elevation="2">
            <v-card class="mx-auto" outlined rounded="lg" min-height="250px">
              <div class="text-right">
                <nuxt-link :to="{ name: 'layout-update-id', params: { id: 9 }}">
                  <edit-button />
                </nuxt-link>
              </div>
              <div class="text-center">
                {{widget_setting['post']?widget_setting['post']['title']:''}}
              </div>
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[8]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[8]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[8]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[8]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </v-card>
          </v-col>
        </v-row>
      </v-card>
      <!-- Row Four -->
      <v-card class="mx-auto ma-5" outlined rounded="lg">
        <v-row>
          <v-col cols="12" sm="9" elevation="2">
            <!--                  1st step-->
            <v-row>
              <v-col cols="12" sm="8" elevation>
                <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
                  <div class="text-right">
                    <nuxt-link :to="{ name: 'layout-update-id', params: { id: 10 }}">
                      <edit-button />
                    </nuxt-link>
                  </div>
                  <div class="text-center">
                    {{widget_setting['post']?widget_setting['post']['title']:''}}
                  </div>
                  <div class="text-center ma-2 col-md-">
                    <template>
                      <v-simple-table dense>
                        <thead>
                          <tr>
                            <th class="text-left">
                              Ttile
                            </th>
                            <th class="text-left">
                              Data
                            </th>
                          </tr>
                        </thead>
                        <tbody class="text-left">
                          <tr>
                            <td>Data Type</td>
                            <td>{{ widgets[9]['data_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Widget Type</td>
                            <td>{{ widgets[9]['widget_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Data Limit</td>
                            <td>{{ widgets[9]['data_limit'] }}</td>
                          </tr>
                          <tr>
                            <td>Status</td>
                            <td>
                              <v-chip v-if="widgets[9]['widget_status'] == 1" color="success" text-color="white" bold>
                                Active
                              </v-chip>
                              <v-chip v-else color="red" text-color="white">
                                Inactive
                              </v-chip>
                            </td>
                          </tr>
                        </tbody>
                      </v-simple-table>
                    </template>
                  </div>
                </v-card>
              </v-col>
              <v-col cols="12" sm="4" elevation>
                <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
                  <div class="text-right">
                    <nuxt-link :to="{ name: 'layout-update-id', params: { id: 11 }}">
                      <edit-button />
                    </nuxt-link>
                  </div>
                  <div class="text-center">
                    {{widget_setting['post']?widget_setting['post']['title']:''}}
                  </div>
                  <div class="text-center ma-2 col-md-">
                    <template>
                      <v-simple-table dense>
                        <thead>
                          <tr>
                            <th class="text-left">
                              Ttile
                            </th>
                            <th class="text-left">
                              Data
                            </th>
                          </tr>
                        </thead>
                        <tbody class="text-left">
                          <tr>
                            <td>Data Type</td>
                            <td>{{ widgets[10]['data_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Widget Type</td>
                            <td>{{ widgets[10]['widget_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Data Limit</td>
                            <td>{{ widgets[10]['data_limit'] }}</td>
                          </tr>
                          <tr>
                            <td>Status</td>
                            <td>
                              <v-chip v-if="widgets[10]['widget_status'] == 1" color="success" text-color="white" bold>
                                Active
                              </v-chip>
                              <v-chip v-else color="red" text-color="white">
                                Inactive
                              </v-chip>
                            </td>
                          </tr>
                        </tbody>
                      </v-simple-table>
                    </template>
                  </div>
                </v-card>
              </v-col>
            </v-row>
            <!--                  2nd Step-->
            <v-row>
              <v-col cols="12" sm="4" elevation>
                <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
                  <div class="text-right">
                    <nuxt-link :to="{ name: 'layout-update-id', params: { id: 13 }}">
                      <edit-button />
                    </nuxt-link>
                  </div>
                  <div class="text-center">
                    {{widget_setting['post']?widget_setting['post']['title']:''}}
                  </div>
                  <div class="text-center ma-2 col-md-">
                    <template>
                      <v-simple-table dense>
                        <thead>
                          <tr>
                            <th class="text-left">
                              Ttile
                            </th>
                            <th class="text-left">
                              Data
                            </th>
                          </tr>
                        </thead>
                        <tbody class="text-left">
                          <tr>
                            <td>Data Type</td>
                            <td>{{ widgets[12]['data_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Widget Type</td>
                            <td>{{ widgets[12]['widget_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Data Limit</td>
                            <td>{{ widgets[12]['data_limit'] }}</td>
                          </tr>
                          <tr>
                            <td>Status</td>
                            <td>
                              <v-chip v-if="widgets[12]['widget_status'] == 1" color="success" text-color="white" bold>
                                Active
                              </v-chip>
                              <v-chip v-else color="red" text-color="white">
                                Inactive
                              </v-chip>
                            </td>
                          </tr>
                        </tbody>
                      </v-simple-table>
                    </template>
                  </div>
                </v-card>
              </v-col>
              <v-col cols="12" sm="8" elevation>
                <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
                  <div class="text-right">
                    <nuxt-link :to="{ name: 'layout-update-id', params: { id: 14 }}">
                      <edit-button />
                    </nuxt-link>
                  </div>
                  <div class="text-center">
                    {{widget_setting['post']?widget_setting['post']['title']:''}}
                  </div>
                  <div class="text-center ma-2 col-md-">
                    <template>
                      <v-simple-table dense>
                        <thead>
                          <tr>
                            <th class="text-left">
                              Ttile
                            </th>
                            <th class="text-left">
                              Data
                            </th>
                          </tr>
                        </thead>
                        <tbody class="text-left">
                          <tr>
                            <td>Data Type</td>
                            <td>{{ widgets[13]['data_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Widget Type</td>
                            <td>{{ widgets[13]['widget_type'] }}</td>
                          </tr>
                          <tr>
                            <td>Data Limit</td>
                            <td>{{ widgets[13]['data_limit'] }}</td>
                          </tr>
                          <tr>
                            <td>Status</td>
                            <td>
                              <v-chip v-if="widgets[13]['widget_status'] == 1" color="success" text-color="white" bold>
                                Active
                              </v-chip>
                              <v-chip v-else color="red" text-color="white">
                                Inactive
                              </v-chip>
                            </td>
                          </tr>
                        </tbody>
                      </v-simple-table>
                    </template>
                  </div>
                </v-card>
              </v-col>
            </v-row>
          </v-col>
          <v-col cols="12" sm="3" elevation="2">
            <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
              <div class="text-right">
                <nuxt-link :to="{ name: 'layout-update-id', params: { id: 12 }}">
                  <edit-button />
                </nuxt-link>
              </div>
              <div class="text-center">
                {{widget_setting['post']?widget_setting['post']['title']:''}}
              </div>
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[11]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[11]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[11]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[11]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </v-card>
          </v-col>
        </v-row>
      </v-card>
      <!-- Row Five -->
      <v-row>
        <v-col cols="12" sm="12" elevation="2">
          <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
            <div class="text-right">
              <nuxt-link :to="{ name: 'layout-update-id', params: { id: 15 }}">
                <edit-button />
              </nuxt-link>
            </div>
            <div class="text-center">
              {{widget_setting['post']?widget_setting['post']['title']:''}}
            </div>
            <div class="text-center ma-2 col-md-">
              <template>
                <v-simple-table dense>
                  <thead>
                    <tr>
                      <th class="text-left">
                        Ttile
                      </th>
                      <th class="text-left">
                        Data
                      </th>
                    </tr>
                  </thead>
                  <tbody class="text-left">
                    <tr>
                      <td>Data Type</td>
                      <td>{{ widgets[14]['data_type'] }}</td>
                    </tr>
                    <tr>
                      <td>Widget Type</td>
                      <td>{{ widgets[14]['widget_type'] }}</td>
                    </tr>
                    <tr>
                      <td>Data Limit</td>
                      <td>{{ widgets[14]['data_limit'] }}</td>
                    </tr>
                    <tr>
                      <td>Status</td>
                      <td>
                        <v-chip v-if="widgets[14]['widget_status'] == 1" color="success" text-color="white" bold>
                          Active
                        </v-chip>
                        <v-chip v-else color="red" text-color="white">
                          Inactive
                        </v-chip>
                      </td>
                    </tr>
                  </tbody>
                </v-simple-table>
              </template>
            </div>
          </v-card>
        </v-col>
      </v-row>
      <!-- Row Six -->
      <v-row>
        <v-col cols="12" sm="12" elevation="2">
          <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
            <div class="text-right">
              <nuxt-link :to="{ name: 'layout-update-id', params: { id: 16 }}">
                <edit-button />
              </nuxt-link>
            </div>
            <div class="text-center">
              Widget Sixteen ( Youtube News Link widget )
            </div>
            <div class="text-center ma-2 col-md-">
              <template>
                <v-simple-table dense>
                  <thead>
                    <tr>
                      <th class="text-left">
                        Ttile
                      </th>
                      <th class="text-left">
                        Data
                      </th>
                    </tr>
                  </thead>
                  <tbody class="text-left">
                    <tr>
                      <td>Data Type</td>
                      <td>{{ widgets[15]['data_type'] }}</td>
                    </tr>
                    <tr>
                      <td>Widget Type</td>
                      <td>{{ widgets[15]['widget_type'] }}</td>
                    </tr>
                    <tr>
                      <td>Data Limit</td>
                      <td>{{ widgets[15]['data_limit'] }}</td>
                    </tr>
                    <tr>
                      <td>Status</td>
                      <td>
                        <v-chip v-if="widgets[15]['widget_status'] == 1" color="success" text-color="white" bold>
                          Active
                        </v-chip>
                        <v-chip v-else color="red" text-color="white">
                          Inactive
                        </v-chip>
                      </td>
                    </tr>
                  </tbody>
                </v-simple-table>
              </template>
            </div>
          </v-card>
        </v-col>
      </v-row>
      <!-- Row Seven -->
      <v-card class="mx-auto ma-5" outlined rounded="lg">
        <v-row>
          <v-col cols="12" sm="3" elevation="2">
            <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
              <div class="text-right">
                <nuxt-link :to="{ name: 'layout-update-id', params: { id: 17 }}">
                  <edit-button />
                </nuxt-link>
              </div>
              <div class="text-center">
                {{widget_setting['post']?widget_setting['post']['title']:''}}
              </div>
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[16]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[16]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[16]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[16]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </v-card>
          </v-col>
          <v-col cols="12" sm="3" elevation="2">
            <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
              <div class="text-right">
                <nuxt-link :to="{ name: 'layout-update-id', params: { id: 18 }}">
                  <edit-button />
                </nuxt-link>
              </div>
              <div class="text-center">
                {{widget_setting['post']?widget_setting['post']['title']:''}}
              </div>
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[17]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[17]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[17]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[17]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </v-card>
          </v-col>
          <v-col cols="12" sm="6" elevation="2">
            <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
              <div class="text-right">
                <nuxt-link :to="{ name: 'layout-update-id', params: { id: 19 }}">
                  <edit-button />
                </nuxt-link>
              </div>
              <div class="text-center">
                Widget Nineteen (Image Slider)
              </div>
              <div class="text-center ma-2 col-md-">
                <template>
                  <v-simple-table dense>
                    <thead>
                      <tr>
                        <th class="text-left">
                          Ttile
                        </th>
                        <th class="text-left">
                          Data
                        </th>
                      </tr>
                    </thead>
                    <tbody class="text-left">
                      <tr>
                        <td>Data Type</td>
                        <td>{{ widgets[18]['data_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Widget Type</td>
                        <td>{{ widgets[18]['widget_type'] }}</td>
                      </tr>
                      <tr>
                        <td>Data Limit</td>
                        <td>{{ widgets[18]['data_limit'] }}</td>
                      </tr>
                      <tr>
                        <td>Status</td>
                        <td>
                          <v-chip v-if="widgets[18]['widget_status'] == 1" color="success" text-color="white" bold>
                            Active
                          </v-chip>
                          <v-chip v-else color="red" text-color="white">
                            Inactive
                          </v-chip>
                        </td>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </template>
              </div>
            </v-card>
          </v-col>
        </v-row>
      </v-card>
      <!-- Row Eight -->
      <v-row>
        <v-col cols="12" sm="12" elevation="2">
          <v-card class="mx-auto" outlined rounded="lg" min-height="245px">
            <div align="right">
              <nuxt-link :to="{ name: 'layout-update-id', params: { id: 20 }}">
                <edit-button />
              </nuxt-link>
            </div>
            <div class="text-center">
              {{widget_setting['footer']?widget_setting['footer']['title']:''}}
            </div>
            <div class="text-center ma-2 col-md-">
              <template>
                <v-simple-table dense>
                  <thead>
                    <tr>
                      <th class="text-left">
                        Ttile
                      </th>
                      <th class="text-left">
                        Data
                      </th>
                    </tr>
                  </thead>
                  <tbody class="text-left">
                    <tr>
                      <td>Data Type</td>
                      <td>{{ widgets[19]['data_type'] }}</td>
                    </tr>
                    <tr>
                      <td>Widget Type</td>
                      <td>{{ widgets[19]['widget_type'] }}</td>
                    </tr>
                    <tr>
                      <td>Data Limit</td>
                      <td>{{ widgets[19]['data_limit'] }}</td>
                    </tr>
                    <tr>
                      <td>Status</td>
                      <td>
                        <v-chip v-if="widgets[19]['widget_status'] == 1" color="success" text-color="white" bold>
                          Active
                        </v-chip>
                        <v-chip v-else color="red" text-color="white">
                          Inactive
                        </v-chip>
                      </td>
                    </tr>
                  </tbody>
                </v-simple-table>
              </template>
            </div>
          </v-card>
        </v-col>
      </v-row>
    </v-col>
    <!-- Layout End -->
    <!-- Skeleton Start -->
    <v-col cols="12" md="4" sm="6">
      <!-- Row One -->
      <v-row>
        <v-col cols="12" sm="12" elevation="2" v-if="widgets[0]['widget_status'] == 1">
          <v-skeleton-loader class="mx-auto" type="list-item-avatar"></v-skeleton-loader>
        </v-col>
      </v-row>
      <!-- Row Two -->
      <v-row>
        <v-col cols="12" sm="12" elevation="2" v-if="widgets[1]['widget_status'] == 1">
          <v-skeleton-loader class="mx-auto mb-1" type="list-item"></v-skeleton-loader>
        </v-col>
      </v-row>
      <!-- Row Three -->
      <v-row>
        <v-col cols="12" sm="3" elevation="2" pa="2" v-if="widgets[3]['widget_status'] == 1">
          <v-sheet class="">
            <v-skeleton-loader class="mx-auto" type="image" height="50px" width="95%"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto pt-2" type="text@2" width="95%"></v-skeleton-loader>
          </v-sheet>

          <v-sheet class="">
            <v-skeleton-loader class="mx-auto" type="image" height="50px" width="95%"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto pt-2" type="text@2" width="95%"></v-skeleton-loader>
          </v-sheet>
        </v-col>
        <v-col cols="12" sm="5" elevation="2" pa="2" v-if="widgets[4]['widget_status'] == 1">
          <v-sheet class="">
            <v-skeleton-loader class="mx-auto" type="list-item" width="80%"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto" type="image" height="50px" width="95%"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto pt-2" type="text@4" width="95%"></v-skeleton-loader>
          </v-sheet>
        </v-col>
        <v-col cols="12" sm="4" elevation="2" pa="2" v-if="widgets[5]['widget_status'] == 1">
          <v-sheet class="">
            <v-skeleton-loader class="mx-auto" type="list-item" width="80%"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto" type="image" height="50px" width="95%"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto pt-2" type="text@4" width="95%"></v-skeleton-loader>
          </v-sheet>
        </v-col>
      </v-row>
      <!-- Row Four -->
      <v-row>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[4]['widget_status'] == 1">
          <v-sheet class="">
            <v-skeleton-loader class="mx-auto" type="list-item-avatar"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto" type="image" height="100px" width="95%"></v-skeleton-loader>
          </v-sheet>
        </v-col>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[5]['widget_status'] == 1">
          <v-sheet class="">
            <v-skeleton-loader class="mx-auto" type="list-item-avatar"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto" type="image" height="100px" width="95%"></v-skeleton-loader>
          </v-sheet>
        </v-col>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[6]['widget_status'] == 1">
          <v-sheet class="">
            <v-skeleton-loader class="mx-auto" type="list-item-avatar"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto" type="image" height="100px" width="95%"></v-skeleton-loader>
          </v-sheet>
        </v-col>
      </v-row>
      <!-- Row Five -->
      <v-row>
        <v-col cols="12" sm="8" elevation="2" v-if="widgets[7]['widget_status'] == 1">
          <v-sheet class="">
            <v-skeleton-loader class="mx-auto pt-2" type="text" width="95%"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto pt-2" type="image" height="70px" width="95%"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto pt-2" type="text@4" width="95%"></v-skeleton-loader>
          </v-sheet>

        </v-col>

        <v-col cols="12" sm="4" elevation="2" v-if="widgets[8]['widget_status'] == 1">
          <v-sheet class="">
            <v-skeleton-loader class="mx-auto" type="list-item-avatar"></v-skeleton-loader>
            <v-skeleton-loader class="mx-auto" type="image" height="100px" width="95%"></v-skeleton-loader>
          </v-sheet>
        </v-col>
      </v-row>
      <!-- Row Six -->
      <v-row>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[9]['widget_status'] == 1">
          <widget-common />

        </v-col>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[10]['widget_status'] == 1">
          <widget-common />
        </v-col>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[11]['widget_status'] == 1">
          <widget-common />
        </v-col>
      </v-row>
      <!-- Row Seven -->
      <v-row>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[12]['widget_status'] == 1">
          <widget-common />
        </v-col>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[13]['widget_status'] == 1">
          <widget-common />
        </v-col>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[14]['widget_status'] == 1">
          <widget-common />
        </v-col>
      </v-row>
      <!-- Row Eight -->
      <v-row>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[15]['widget_status'] == 1">
          <widget-common />
        </v-col>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[16]['widget_status'] == 1">
          <widget-common />
        </v-col>
        <v-col cols="12" sm="4" elevation="2" v-if="widgets[17]['widget_status'] == 1">
          <widget-common />
        </v-col>
      </v-row>
      <!-- Row Nine -->
      <v-row>
        <v-col cols="12" sm="12" elevation="2" v-if="widgets[18]['widget_status'] == 1">
          <v-skeleton-loader class="mx-auto" type="list-item-avatar"></v-skeleton-loader>
        </v-col>
      </v-row>
      <!-- Row Ten -->
      <v-row>
        <v-col cols="12" sm="12" elevation="2" v-if="widgets[19]['widget_status'] == 1">
          <v-sheet class="d-flex ">
            <v-col cols="12" sm="4">
              <v-skeleton-loader class="mx-auto" type="text@2"></v-skeleton-loader>
            </v-col>
            <v-col cols="12" sm="4">
              <v-skeleton-loader class="mx-auto" type="text@2"></v-skeleton-loader>
            </v-col>
            <v-col cols="12" sm="4">
              <v-skeleton-loader class="mx-auto" type="text@2"></v-skeleton-loader>
            </v-col>
          </v-sheet>
        </v-col>
      </v-row>
    </v-col>
    <!-- Row End -->
  </v-row>
</v-container>
</template>

<script>
export default {
  data: () => ({
    widgets: [],
    layouts: [
      'Layout One', 'Layout Two', 'Layout Three', 'Layout Four', 'Layout Five',
      'Layout Six', 'Layout Seven', 'Layout Eight', 'Layout Nine', 'Layout Ten',
    ],
    widget_setting: [],

  }),

  created() {

    this.getWidget();
  },

  methods: {
    async getWidgets() {
      try {
        const {
          data
        } = await this.$axios.get('/widgets/create');
        this.widgets = data;
      } catch (e) {
        this.error = e.data;
      }
    },

    async getWidget() {

      try {
        const {
          data
        } = await this.$axios.get('/widget/setting');

        this.widget_setting = data;

      } catch (e) {
        this.error = e.data;
      }
    },
  },

  asyncData(context) {
    const AuthStr = 'Bearer '.concat(context.$auth.strategy.token.get());
    return context.$axios
      //.get(context.env.apiRoot + 'post-slug?slug=' + encodeURI(context.params.slug))
      .get('/layouts/' + context.params.id + '/edit', {
        headers: {
          Authorization: AuthStr
        }
      })
      .then((res) => {
        if (res.data.length === 0 || res.data.error) {
          throw ({
            statusCode: 404,
            message: 'Widgets not found'
          })
        }
        // console.log(res.data);
        return {
          widgets: res.data
        }
      })
      .catch(error => {
        if (error.response) {
          // Request made and server responded
          //this.errorResponse = error.response.data;
          this.errorCode = error.response.status;
        } else if (error.request) {
          // The request was made but no response was received
          //console.log(error.request);
        } else {
          // Something happened in setting up the request that triggered an Error
          return {
            error: error.message
          };
          return context.error({
            statusCode: 500,
            message: error.message
          })
        }
      });
  },
}
</script>

<style>
a {
  text-decoration: none;
}

.v-data-table {
  line-height: 3;
}
</style>
