---
title: "Common Errors"
linkTitle: "Common Errors"
weight: 6
description: >
  COMMON METADATA ERRORS - UK Location Discovery Metadata Service
---

{{% pageinfo %}}
This is a placeholder page that shows you how to use this template site.
{{% /pageinfo %}}

# Introduction
<p>The UK Location Discovery Metadata Service (DMS) lies at the heart of UK Location and the delivery of the UK Location Strategy and INSPIRE - 'to know what data we have'.</p>
<p>The DMS operates by collecting valid metadata records from data publishers and making them available on data.gov.uk, and for further collection to the European INSPIRE Geoportal.</p>

## Target Audience

<p>The primary audience for this document are those responsible for creating and maintaining metadata records, located within data provider organisations, and their technical partners.</p>

## Background

<p>This document is largely based on an analysis of validation failures when metadata validation was first run on the records that had already been collected into <a title="https://data.gov.uk/" href="https://data.gov.uk/" target="_blank" rel="alternate noopener noreferrer">data.gov.uk</a>. Approximately half the records present in data.gov.uk at that time initially failed.</p>

## Assumed Knowledge

<p>This guide assumes that the reader is familiar with the creation and management of metadata and has read the <a title="Getting started guides" href="https://data.gov.uk/location/guidance_and_tools" rel="alternate">UK Location “Getting Started' series of guides</a> [<a title="References" href="/agi-groups/standards-committee/uk-gemini/40-gemini/1047-metadata-guidelines-for-geospatial-data-resources-part-3" target="_blank" rel="alternate noopener noreferrer">27</a>], and the DMS Operational Guide.</p>
<p>Readers requiring an introduction to discovery metadata for geospatial data resources are referred to the UK GEMINI guide “Metadata Guidelines for Geospatial Data Resources, Introduction – Part 1” [<a title="References" href="/agi-groups/standards-committee/uk-gemini/40-gemini/1047-metadata-guidelines-for-geospatial-data-resources-part-3" target="_blank" rel="alternate noopener noreferrer">1</a>].</p>
<p>Other useful reading includes AGI’s Guidelines for UK GEMINI Part 3 Metadata Quality</p>
<p><strong>GEMINI 2.3 note: the DMS Operational Guide, UK GEMINI Encoding Guidance and AGI's Guidelines - Part 2 have all been consolidated into this content.<br /></strong></p>

## Where to Obtain More Information

<p>The latest information, and additional resources, can be obtained by visiting the <a href="http://data.gov.uk/location">UK Location</a> web site.</p>
<p>If you would like to contact the UK Location Coordination Unit, contact details are at <a href="http://data.gov.uk/location/contact_points">http://data.gov.uk/location/contact_points</a></p>

## Validation

### GEMINI 2.3

<p><span style="font-weight: 400;">There is no currently no validation tool for GEMINI 2.3, but some software companies are developing tools.  To validate a metadata record in your own software you should:</span></p>
<ul>
<li><span style="font-weight: 400;"> Validate using the ISO 19139 (APISO) schemas.  (</span><a href="http://inspire.ec.europa.eu/draft-schemas/inspire-md-schemas/apiso-inspire/apiso-inspire.xsd"><span style="font-weight: 400;">http://inspire.ec.europa.eu/draft-schemas/inspire-md-schemas/apiso-inspire/apiso-inspire.xsd</span></a><span style="font-weight: 400;">)</span></li>
<li><span style="font-weight: 400;">Validate for additional requirements using the GEMINI 2.3 Schematron Schema, which is available at </span><a href="/about/resources/category/125-schematron"><span style="font-weight: 400;">https://www.agi.org.uk/about/resources/category/125-schematron.</span></a></li>
</ul>
<p><span style="font-weight: 400;"> It doesn't matter which order validation is done in, but to be valid, records must validate against both the APISO schema and the GEMINI 2.3 Schematron.</span></p>
<p><span style="font-weight: 400;">In addition a second (supplemental) schematron is provided to test for recommendations in your metadata structure.</span></p>

### GEMINI 2.2 and data.gov.uk

<p>Currently, validating a UK Location metadata (GEMINI 2.2) record is a three stage process:</p>
<ul>
<li>First, a metadata set is validated against the ISO 19139 schemas. UK Location / data.gov.uk use the XSD files provided by EDEN; see <a title="Encoding Guidance" href="/agi-groups/standards-committee/uk-gemini/40-gemini/1048-uk-gemini-encoding-guidance" target="_blank" rel="alternate noopener noreferrer"><em>UK GEMINI Encoding Guidance </em></a>for details.</li>
<li>If the metadata set proves to be schema valid, it is then validated against the ISO 19139 Table A.1 Constraints Schematron schema. The Schematron schema relies on hardcoded XPath statements which will only work effectively on a schema valid XML set.</li>
<li>Finally, if the XML is still valid it is validated against the GEMINI2 Profile Schematron schema.</li>
</ul>
<p>Any failure of this validation is logged for attention by the administrator of the harvest source. The record is loaded into data.gov.uk, assuming it passes a very minimal subset.</p>
<p>This is expected to change before late 2019, to only accept GEMINI 2.3 records.</p>

### European INSPIRE Geoportal

<p>The European INSPIRE Geoportal carries out its own validation. This uses basically the same rules. No records are rejected, but errors are reported, at <a href="https://inspire-geoportal.ec.europa.eu/proxybrowser/">inspire-geoportal.ec.europa.eu/proxybrowser/.</a></p>

### Warnings, soft errors, recommendations

<p>Even where the metadata is valid, there can be 'soft errors', where the metadata may be misleading.</p>
<p>With GEMINI 2.3, <span style="font-weight: 400;">a second (supplemental) schematron is provided to test for recommendations.</span></p>

# Schema errors

## Confusion of Date and DateTime

<p>In ISO 19115, Date and DateTime are distinct types. Although in many elements, either is allowed, the XML encoding needs to be explicit about which is given. It is an error to put a date (such as 2010-05-12) in a DateTime element.</p>
<p>Example of invalid structure:</p>
<p><code>&lt;gmd:dateStamp&gt;</code></p>
<p><code><strong>            </strong>&lt;gco:DateTime&gt;<span style="color: black;">2012-11-15</span>&lt;/gco:DateTime&gt;</code></p>
<p><code>&lt;/gmd:dateStamp&gt;</code></p>
<p>Examples of valid structure:</p>
<p>This should either include the time, e.g.</p>
<p><code>&lt;gmd:dateStamp&gt;</code></p>
<p><code><strong>            </strong>&lt;gco:DateTime&gt;<span style="color: black;">2012-11-15T13:50:38</span>&lt;/gco:DateTime&gt;</code></p>
<p><code>&lt;/gmd:dateStamp&gt;</code></p>
<p>Or be explicit that it doesn’t:</p>
<p><code>&lt;gmd:dateStamp&gt;</code></p>
<p><code><strong>            </strong>&lt;gco:Date&gt;<span style="color: black;">2012-11-15</span>&lt;/gco:Date&gt;</code></p>
<p><code>&lt;/gmd:dateStamp&gt;</code></p>
<h3>2.2 Elements in the wrong order</h3>
<p>Although there is no “logical” ordering of the elements in ISO 19115, INSPIRE, or GEMINI, the XML pattern adopted by ISO 19139 means that the elements must appear in the correct order. The order enforced is the order the elements appear in ISO 19115; the GEMINI Encoding Guidance contains an appendix giving the correct order for the subset of elements used by GEMINI.</p>
<p>The example found contained the ISO 19115 metadata characterSet element before the metadata language element.</p>
<h2><a id="ISO_errors"></a>3. ISO 19139 Schematron errors</h2>
<p>See also <a title="Empty Strings" href="#soft_errors" rel="alternate">“Empty strings”</a>.</p>
<h3>3.1 No level description</h3>
<p>ISO 19115 requires that a “level description” is given for any quality statement that is not describing the “dataset” or “series” level. INSPIRE and GEMINI use the quality statement for both lineage and conformity. This means that any “service” record must provide a gmd:DQ_Scope/gmd:levelDescription element, such as:</p>
<p><code>&lt;gmd:DQ_Scope&gt;</code></p>
<p><code>          &lt;gmd:level&gt;</code></p>
<p><code>                   &lt;gmd:MD_ScopeCode codeList=<span style="color: #3366ff;">"http://standards.iso.org/ittf/PubliclyAvailableStandards/ISO_19139_Schemas/resources/codelist/gmxCodelists.xml#MD_ScopeCode"</span> codeListValue="service"&gt;service&lt;/gmd:MD_ScopeCode&gt;</code></p>
<p><code>          &lt;/gmd:level&gt;</code></p>
<p><code>          &lt;gmd:levelDescription&gt;</code></p>
<p><code>                   &lt;gmd:MD_ScopeDescription&gt;</code></p>
<p><code>                             &lt;gmd:other&gt;</code></p>
<p><code>                                      &lt;gco:CharacterString&gt;<span style="color: black;">Geographic web service</span>&lt;/gco:CharacterString&gt;</code></p>
<p><code>                             &lt;/gmd:other&gt;</code></p>
<p><code>                   &lt;/gmd:MD_ScopeDescription&gt;</code></p>
<p><code>          &lt;/gmd:levelDescription&gt;</code></p>
<p><code>&lt;/gmd:DQ_Scope&gt;</code></p>
<p>A similar rule applies to “hierarchyLevelName”, which must be provided for any record that is not describing a dataset.</p>
<h3>3.4 No Format provided</h3>
<p>ISO 19139 requires that a format is given, either within the “distribution” section or the “distributor” section. INSPIRE &amp; UK GEMINI encoding guidance only expects the distribution section, as the place to encode the Resource locator, which effectively renders distribution format mandatory.</p>
<h2><a id="proc_errors"></a>4. Processing errors</h2>
<p>These errors do not result in invalid records on an individual basis, but may well result in the wrong records being available to the public.</p>
<h3>4.1 Non-compliant Web Accessible Folder (WAF)</h3>
<p>The collection definition is very precise. Just because you can browse to a page that appears to contain the records, it does not mean that the system can collect from them. For example, the page may just contain links to records that are elsewhere.</p>
<p>Similarly, collection differentiates between a single XML record at the end of a URL, and a WAF.</p>
<h3>4.2 FileIdentifier</h3>
<p>This is the identifier for a metadata record through time, so do ensure that it remains the same when you update a record, and is different in each record you create.</p>
<p>If you accidently change the identifier, the new record will not replace the old one.</p>
<p>If you accidently provide two records with the same identifier, one will replace the other.</p>
<h3>4.3 Metadata date</h3>
<p>This is used to distinguish which of two records with the same fileIdentifier the system will keep.</p>
<p>Even if the records are moved to a different server, if the fileIdentifier and metadata date are the same, the harvester will not collect the new files.</p>
<h2><a id="inspire_warnings"></a>5. European INSPIRE Geoportal errors &amp; warnings</h2>
<h3>5.1 Conformity statement missing</h3>
<p>INSPIRE requires a ‘conformity’ statement, which can say that the resource conforms, does not conform, or has not been evaluated against, a specification. This is encoded with an ISO 19115 quality report. The INSPIRE encoding guidelines say that “not evaluated” should be encoded by leaving out the quality report. For this reason, GEMINI says that it is conditional, “required if claiming conformance to INSPIRE”.</p>
<p>However, the INSPIRE Geoportal reports a validation issue if the element is missing: “The metadata element "Conformity" is missing, empty or incomplete but it is required”. This can be ignored.</p>
<p><strong>GEMINI Consolidation Note: The INSPIRE Encoding Guidelines were updated in 2013; GEMINI 2.3 will be updated on this point.</strong></p>
<h3>5.2 Missing “coupled resource”</h3>
<p>INSPIRE requires “Coupled resource” to be populated “where relevant”. This effectively makes it mandatory for View &amp; Download services, and the INSPIRE Geoportal reports this as a validation issue. However, the Geoportal also reports this issue for a Discovery service metadata record, where coupled resource is not mandatory.</p>
<h2><a id="soft_errors"></a>6. “Soft” errors</h2>
<h3>6.1 Empty strings</h3>
<p>When first run, approximately half the rejections were down to this error. UK Location decided to remove this check, so the records can be harvested, although it is strongly recommended that this structure is avoided.</p>
<p>ISO 19139 clause A.2.1 states “a property element following the default XCPT pattern is designed to have content (by-value) or attributes (by-reference or NULL with reason).” In context, this states that (with very few exceptions) no metadata element shall be entirely empty: it will either have (valid) content, or it will have a gco:nilReason attribute stating why the content is absent. If the element is optional, it shall be entirely absent from the XML document, not “present but empty”.</p>
<p>The most common examples were structures like:</p>
<p><code>&lt;gmd:phone&gt;</code></p>
<p><code><strong>            </strong>&lt;gmd:CI_Telephone/&gt;</code></p>
<p><code>&lt;/gmd:phone&gt;</code></p>
<p>(in this case, as gmd:phone is optional, it should be entirely missing)</p>
<p>and</p>
<p><code>&lt;gmd:administrativeArea gco:nilReason="<span style="color: #3366ff;">missing</span>"&gt;</code></p>
<p><code><strong>            </strong>&lt;gco:CharacterString/&gt;</code></p>
<p><code>&lt;/gmd:administrativeArea&gt;</code></p>
<p>Examples of valid structures are:</p>
<p><code>&lt;gmd:administrativeArea gco:nilReason="<span style="color: #3366ff;">missing</span>"/&gt;</code></p>
<p>(although again, it would be equally valid to leave the element out entirely)</p>
<p><code>&lt;gmd:deliveryPoint&gt;</code></p>
<p><code><strong>            &lt;</strong>gco:CharacterString&gt;<span style="color: black;">Explorer House, Adanac Drive</span>&lt;/gco:CharacterString&gt;</code></p>
<p><code>&lt;/gmd:deliveryPoint&gt;</code></p>
<h3>6.2 Short relative URLs</h3>
<p>The issues discussed here have just been noted whilst browsing the records in data.gov.uk</p>
<p>Quite a lot of records use the ISO 19115 element “browseGraphic”, which could usefully provide a quick visualisation of the dataset. However, mostly these are populated with a local path, which is then impossible to use once the dataset is harvested to any other location – even if it did work in the data publisher’s original location. For example:</p>
<p><code>&lt;gmd:MD_BrowseGraphic&gt;</code></p>
<p><code><strong>            </strong>&lt;gmd:fileName&gt;</code></p>
<p><code><strong>                        </strong>&lt;gco:CharacterString&gt;<span style="color: black;">Council_Housing_s.png</span>&lt;/gco:CharacterString&gt;</code></p>
<p><code><strong>            </strong>&lt;/gmd:fileName&gt;</code></p>
<p><code><strong>            …</strong></code></p>
<p><code>&lt;/gmd:MD_BrowseGraphic&gt;</code></p>
<h3>6.3 Incorrect code list URL</h3>
<p>The INSPIRE encoding guidance, and therefore earlier versions of the GEMINI Encoding Guidance had a minor spelling (capitalisation) mistake in the path for the code list dictionary. This is used a number of times in most records.</p>
<p><code>&lt;gmd:CI_OnLineFunctionCode codeList<strong>="</strong>http://standards.iso.org/ittf/PubliclyAvailableStandards/ISO_19139_Schemas/resources/Codelist/gmxCodelists.xml#CI_OnLineFunctionCode<strong>" </strong>codeListValue<strong>="</strong>information<strong>"</strong>&gt;information&lt;/gmd:CI_OnLineFunctionCode&gt;</code></p>
<p>Should be</p>
<p><code>&lt;gmd:CI_OnLineFunctionCode codeList<strong>="</strong>http://standards.iso.org/ittf/PubliclyAvailableStandards/ISO_19139_Schemas/resources/codelist/gmxCodelists.xml#CI_OnLineFunctionCode<strong>" </strong>codeListValue<strong>="</strong>information"&gt;information&lt;/gmd:CI_OnLineFunctionCode&gt;</code></p>
<p>(a lower case ‘c’ in the first occurrence of ‘codelist’ within the URL)</p>
<p><strong>GEMINI Consolidation Note: The INSPIRE Encoding Guidelines have been updated to correct this, in 2016.</strong><br /><br /></p>
<h2><a id="winner"></a>7. And the winner?</h2>
<p>This table, for interest, gives the approximate error rate for each of the above errors, in the sample tested in late 2012. This does not include those soft errors only found by inspection.</p>
<table>
<tbody>
<tr>
<td width="308">
<p><span style="font-size: 10pt;"><strong>Error</strong></span></p>
</td>
<td width="308">
<p><span style="font-size: 10pt;"><strong>Proportion</strong></span></p>
</td>
</tr>
<tr>
<td width="308">
<p>Empty strings</p>
</td>
<td width="308">
<p>50%</p>
</td>
</tr>
<tr>
<td width="308">
<p>No level description</p>
</td>
<td width="308">
<p>25%</p>
</td>
</tr>
<tr>
<td width="308">
<p>No format</p>
</td>
<td width="308">
<p>24%</p>
</td>
</tr>
<tr>
<td width="308">
<p><em>Four other errors, one occurrence each</em></p>
</td>
<td width="308">

</td>
</tr>
</tbody>
</table>