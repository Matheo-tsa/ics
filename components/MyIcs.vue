<template>
  <div>
    <button @click="initIcs">RDV</button>
  </div>
</template>

<script>
import { VCALENDAR, VEVENT } from 'ics-js';

export default {
  name: 'MyIcs',
  methods: {
    initIcs () {
      const cal = new VCALENDAR();
      const event = new VEVENT();
      event.addProp('UID');
      event.addProp('DTSTAMP', new Date('2021-11-02 10:00:00'), { VALUE: 'DATE-TIME' });
      // Date et heure de début
      event.addProp('DTSTART', new Date('2021-12-02 11:11:00'), { VALUE: 'DATE-TIME' });
      // Date et heure de fin
      event.addProp('DTEND', new Date('2021-12-02 12:12:00'), { VALUE: 'DATE-TIME' });
      event.addProp('ATTENDEE', null, {
        CN: 'ArteBeaute',
        RSVP: 'FALSE:mailto:contact@artebeaute.com',
        Title: 'Titre de lattendee'
      });

      // Titre de l'evenement
      event.addProp('SUMMARY', 'TITRE DE LEVENT');
      // Description de l'evenement
      event.addProp('DESCRIPTION', 'DESCRIPTION DE LEVENT');
      // Localisation de l'evenement (peut renvoyer vers un service de navigation)
      event.addProp('LOCATION', 'Rue maréchal férrand');
      // Localisation (supposée métadonnée)
      event.addProp('GEO', '48.856614;2.3522219');

      cal.addProp('VERSION', 2);
      cal.addProp('PRODID', 'ArteBeauté');
      cal.addComponent(event);
      cal.toString();
      console.log(cal.toString());

      // Sauvegarde du fichier
      const FileSaver = require('file-saver');
      const file = new File([cal.toString()], "mon-rdv.ics", {type: "text/plain;charset=utf-8"});
      FileSaver.saveAs(file);
    }
  }
}
</script>

<style scoped>
  *{
    font-family: Poppins, sans-serif;
  }
</style>
