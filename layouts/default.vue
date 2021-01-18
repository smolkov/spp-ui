<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <template v-for="(item, i) in items">
          <template v-if="item.items && item.items.length > 0">
            <v-list-group :key="i" no-action :to="item.to">
              <template v-slot:activator>
                <v-list-item-action>
                  <v-icon>{{ item.icon }}</v-icon>
                </v-list-item-action>
                <v-list-item-content>
                  <v-list-item-title v-text="item.title"></v-list-item-title>
                </v-list-item-content>
              </template>
              <v-list-item
                v-for="subitem in item.items"
                :key="subitem.name"
                :to="subitem.to"
                router
                exact
              >
                <v-list-item-content>
                  <v-list-item-title v-text="subitem.title" />
                </v-list-item-content>
              </v-list-item>
            </v-list-group>
          </template>
          <template v-else>
            <v-list-item :key="i" :to="item.to" router exact>
              <v-list-item-action>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-action>
              <v-list-item-content>
                <v-list-item-title v-text="item.title" />
              </v-list-item-content>
            </v-list-item>
          </template>
        </template>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-btn icon @click.stop="fixed = !fixed">
        <v-icon>mdi-minus</v-icon>
      </v-btn>
      <v-tabs v-model="tab">
        <v-tab to="/"> Schutz </v-tab>
        <v-tab to="/led"> LED </v-tab>
        <v-tab to="/relais"> Relais </v-tab>
        <v-tab to="/kmd"> Kmd.->Engaunge (vBE)</v-tab>
        <v-tab to="/inputs"> Eingaenge </v-tab>
        <v-tab to="/tests"> Tests </v-tab>
      </v-tabs>
      <v-spacer />
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>mdi-menu</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light> mdi-repeat </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Dashboard',
          to: '/',
        },
        {
          icon: 'mdi-chip',
          title: 'Firmenware anpassung',
          to: '/firmware/firmwareanpassung',
        },
        {
          icon: 'mdi-chip',
          title: 'Objectanpassung',
          items: [
            {
              title: 'Gerautanpassung',
              to: '/objectanpassung/device',
            },
            {
              title: 'LS-Anpassung',
              to: '/objectanpassung/ls',
            },
            {
              title: 'Wandleranpassung',
              to: '/objectanpassung/wandler',
            },
            {
              title: 'Wertesatz',
              to: '/objectanpassung/wertesatz',
            },
          ],
        },
        {
          icon: 'mdi-console-network',
          title: 'Netzanpassung',
          items: [
            {
              title: 'Netzanpassung',
              to: '/netzanpassung/net',
            },
          ],
        },
        {
          icon: 'mdi-robot',
          title: 'Schutzfunktionen',
          items: [
            {
              title: 'AFE Schutz',
              to: '/functions/afeschutz',
            },
            {
              title: 'AWE',
              to: '/functions/awe',
            },
            {
              title: 'diesanregung',
              to: '/functions/diesanregung',
            },
            {
              title: 'differentialschutz',
              to: '/functions/differentialschutz',
            },
            {
              title: 'dimeldestufen',
              to: '/functions/dimeldestufen',
            },
            {
              title: 'einschaltschutz',
              to: '/functions/einschaltschutz',
            },
            {
              title: 'erddiffshutz',
              to: '/functions/erddiffshutz',
            },
            {
              title: 'erdschlusserfassung',
              to: '/functions/erdschlusserfassung',
            },
            {
              title: 'fehlerortbestiemung',
              to: '/functions/fehlerortbestiemung',
            },
            {
              title: 'freqanderungsschutz',
              to: '/functions/freqanderungsschutz',
            },
            {
              title: 'generalanregung',
              to: '/functions/generalanregung',
            },
            {
              title: 'ieumzamz',
              to: '/functions/ieumzamz',
            },
            {
              title: 'ilumzamz',
              to: '/functions/ilumzamz',
            },
            {
              title: 'impulsstufe',
              to: '/functions/impulsstufe',
            },
            {
              title: 'inrushstabilisierung',
              to: '/functions/inrushstabilisierung',
            },
            {
              title: 'inrushstabilisierung',
              to: '/functions/inrushstabilisierung',
            },
            {
              title: 'leistungsschutz',
              to: '/functions/leistungsschutz',
            },
            {
              title: 'lsaus',
              to: '/functions/lsaus',
            },
            {
              title: 'lsversageschutz',
              to: '/functions/lsversageschutz',
            },
            {
              title: 'messwertprufung',
              to: '/functions/messwertprufung',
            },
            {
              title: 'pendelschutz',
              to: '/functions/pendelschutz',
            },
            {
              title: 'quschutz',
              to: '/functions/quschutz',
            },
            {
              title: 'rchtungsentscheid',
              to: '/functions/rchtungsentscheid',
            },
            {
              title: 'resrve',
              to: '/functions/resrve',
            },
            {
              title: 'schleifenbestimmung',
              to: '/functions/schleifenbestimmung',
            },
            {
              title: 'signalubertragung',
              to: '/functions/signalubertragung',
            },
            {
              title: 'spannungschutz',
              to: '/functions/spannungschutz',
            },
            {
              title: 'stromgegensystem',
              to: '/functions/stromgegensystem',
            },
            {
              title: 'strommeldestufen',
              to: '/functions/strommeldestufen',
            },
            {
              title: 'synchroncheck',
              to: '/functions/synchroncheck',
            },
            {
              title: 'ubererregungsstabil',
              to: '/functions/ubererregungsstabil',
            },
            {
              title: 'uberlastschutz',
              to: '/functions/uberlastschutz',
            },
            {
              title: 'wiedereinschaltsperre',
              to: '/functions/wiedereinschaltsperre',
            },
            {
              title: 'zanregung',
              to: '/functions/zanregung',
            },
          ],
        },
        {
          icon: 'mdi-directions-fork',
          title: 'EDIR',
          items: [
            {
              title: 'Allgemein',
              to: '/edir/general',
            },
          ],
        },
        {
          icon: 'mdi-ballot',
          title: 'Allgemein',
          items: [
            {
              title: 'Schutz Ein|Aus',
              to: '/allgemein/schutzeinaus',
            },
            {
              title: 'Ausgange',
              to: '/allgemein/ausgaenge',
            },
            {
              title: 'Eingange',
              to: '/allgemein/eingaenge',
            },
            {
              title: 'Goose',
              to: '/allgemein/goose',
            },
            {
              title: 'Resurve',
              to: '/allgemein/resurve',
            },

            {
              title: 'Stoerdatenaufzeichnung',
              to: '/allgemein/stoerdatenaufzeichnung',
            },
            {
              title: 'Virtuelle Eingaenge',
              to: '/allgemein/virtuelleeingaenge',
            },
            {
              title: 'Warnungsstoutung',
              to: '/allgemein/warnungstourung',
            },
            {
              title: 'Weiteres',
              to: '/allgemein/weiteres',
            },
          ],
        },
        {
          icon: 'mdi-ballot',
          title: 'Kommunikation',
          items: [
            {
              title: 'Kommunikation',
              to: '/kommunikation/kommunikation',
            },
            {
              title: 'Leittechnik',
              to: '/kommunikation/leittechnik',
            },
            {
              title: 'wirkschnittstelle',
              to: '/kommunikation/wirkschnittstelle',
            },
          ],
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Schutz',
      tab: null,
    }
  },
}
</script>
