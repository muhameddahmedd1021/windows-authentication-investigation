# Collection and saved settings

- [Windows inputs](windows-inputs.conf) select the Windows channels collected by Universal Forwarder.
- [Forwarder output](windows-outputs.conf) sends them to the lab receiver.
- [Field extraction](splunk-props.conf) and [sharing metadata](splunk-default.meta) expose the XML event fields used in the searches.
- [Alert settings](repeated-failures-alert.json) record the tested internal alert and its final stopped schedule.

The collection uses `lab_windows` and `soc:windows:xml`. The [dashboard definition](../dashboard/authentication-investigation.xml) uses the same searches as the investigation tables.
