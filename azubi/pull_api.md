## AZUBI Pull API

Our application is able to process data streams served via HTTP of different format. If you already have your
jobs wrapped into a custom data stream ready to read via HTTP, please [contact our team](mailto:api@absolventa.de) to verify
if we can handle it.

### Sample Data Format

Here's an ideal XML feed for our application AZUBI.DE. If you are able to provide your job
data in this format, we can immediately configure a connection:

```XML
<?xml version='1.0' encoding='utf-8' ?>
<job_offers type='array'>
  <job_offer>
    <external_id>145-D-22</external_id>
    <mode>standard</mode>
    <title>Ausbildung Bankkaufmann/-frau</title>
    <started_at type='datetime'>
      2017-07-07T00:00:00+02:00
    </started_at>
    <apprenticeship_started_at type='datetime'>
      2017-07-07T00:00:00+02:00
    </started_at>
    <external_url>
      <![CDATA[http:/example.com/jobs/145-D-22]]>
    </external_url>
    <application_url>
      <![CDATA[http://www.example.com/jobs/145-D-22/apply]]>
    </application_url>
    <description>
      <![CDATA[Lorem Ipsum]]>
    </description>
    <company_description>
      <![CDATA[Lorem Ipsum]]>
    </company_description>
    <!--Possible values for minimal degree:  -->
    <!-- basic (Hauptschulabschluss)  -->
    <!-- certificate (Mittlere Reife)  -->
    <!-- graduation ([Fach-]Abitur)  -->
    <minimal_degree>basic</minimal_degree>
    <duration>36</duration><!-- months -->
    <contact_name>Rosi Beckers</contact_name>
    <job_offer_locations type='array'>
      <job_offer_location>
        <street>Friedrichstrasse 67</street>
        <zip>10117</zip>
        <city>Berlin</city>
        <country>Deutschland</country>
        <vacancies>3</vacancies>
      </job_offer_location>
    </job_offer_locations>
  </job_offer>
  <job_offer>
    ...
  </job_offer>
</job_offers>
```
### Data fields

<table>
  <thead>
    <tr>
      <th>attribute</th>
      <th>value</th>
      <th>type</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>external_id</td>
      <td>Your internal identifier of the record</td>
      <td>String</td>
      <td>required</td>
    </tr>
    <tr>
      <td>mode</td>
      <td>
        Possible values: <code>standard</code> and <code>premium</code>.
        Defaults to <code>standard</code> if omitted.
        Cannot be changed after creation.
      </td>
      <td>String</td>
      <td>optional</td>
    </tr>
    <tr>
      <td>title</td>
      <td>Title</td>
      <td>String</td>
      <td>required</td>
    </tr>
    <tr>
      <td>external_url</td>
      <td>
        URL pointing to a HTML representation of your job offer. The HTML content of the <code>external_url</url> will be
        displayed within an <code>iframe</code> element on our website.
      </td>
      <td>String</td>
      <td>optional</td>
    </tr>
    <tr>
      <td>description</td>
      <td>Description text of your job ad. Simple HTML tags such as <code>strong, em, u, ol, ul, li, p, br, a</code> are allowed.</td>
      <td>Text</td>
      <td>required</td>
    </tr>
    <tr>
      <td>company_description</td>
      <td>Description text of your company. Simple HTML tags such as <code>strong, em, u, ol, ul, li, p, br, a</code> are allowed.</td>
      <td>Text</td>
      <td>optional</td>
    </tr>
    <tr>
      <td>started_at</td>
      <td>
        Date the job offer starts being published to our platform. Note that once the job offer has
        been published this field cannot be edited any longer. If left out, we immediately publish your
        job offer.
      </td>
      <td>Datetime</td>
      <td>optional</td>
    </tr>
    <tr>
      <td>apprenticeship_started_at</td>
      <td>Date on which the apprenticeship will start</td>
      <td>Datetime</td>
      <td>optional</td>
    </tr>
    <tr>
      <td>ended_at</td>
      <td>Date on which the job offer stops being published to our platform.</td>
      <td>Datetime</td>
      <td>optional</td>
    </tr>
    <tr>
      <td>trainee_gefluester</td>
      <td>
        <p>Allows co-publication a job offer on our job board TRAINEE-GEFLÜSTER by supplying <code>true</code> (valid TRAINEE-GEFLÜSTER contract required).</p>
        <p>Contact your account manager if you are interested in this service.</p>
      </td>
      <td>String</td>
      <td>optional</td>
    </tr>
    <tr>
      <td>application_url</td>
      <td>URL pointing to the application online formular of the job offer.</td>
      <td>String</td>
      <td>optional (You need to provide either an <code>application_url</code> or an <code>application_email</code>)</td>
    </tr>
    <tr>
      <td>application_email</td>
      <td>E-Mail address potential candidates shall send their applications to</td>
      <td>String</td>
      <td>optional (You need to provide either an <code>application_url</code> or an <code>application_email</code>)</td>
    </tr>
    <tr>
      <td>job_offer_locations</td>
      <td>
        List of job_offer_location objects. Each job_offer_location contained in the list
        has to include at least a <code>city</code> and a <code>zip</code> value.
      </td>
      <td>job_offer_location object</td>
      <td>optional</td>
    </tr>
    <tr>
      <td>use_responsive_template</td>
      <td>
        If you also submit an HTML representation of the job_offer (by submission of
        <code>external_url</code>) and if your HTML representation behaves responsive, you
        can set this attribute to <code>true</code>. In this case the iframe serving
        your HTML content will be displayed for mobile devices, too. If left out or
        set to false, we will always render a text representation of the job offer.
      </td>
      <td>Boolean</td>
      <td>optional</td>
    </tr>
    <tr>
      <td>height</td>
      <td>Height of the iframe displaying the content of <code>external_url</code> in px.</td>
      <td>Integer</td>
      <td>optional</td>
    </tr>
    <tr>
      <td>
        <span class='label label-info'>duration</span>
      </td>
      <td>
        Duration of the apprenticeship in months.
      </td>
      <td>Integer</td>
      <td>optional</td>
    <tr>
      <td>minimal_degree</td>
      <td>
        Minimal graduation degree the candidates should own.
        Possible values:
        <ul>
          <li><code>basic</code> (Hauptschulabschluss)</li>
          <li><code>certificate</code> (Mittlere Reife)</li>
          <li><code>graduation</code> ([Fach-]Abitur)</li>
        </ul>
      </td>
      <td>String</td>
      <td>optional</td>
    </tr>
  </tbody>
</table>
