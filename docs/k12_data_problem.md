# The K12 Data Problem

In your typical school district, student data is being created in more platforms than ever before. The student information system (SIS) is the system of record that contains student demographics and enrollment information. It typically also includes attendance and some, if not all, student grades. A learning management system (LMS) holds student assignment information and often have their own gradebook. Assessment platforms may be utilized for interim and normed assessment data. Beyond that there may also be many classroom focused edTech applications in use.

This results in the district's student data siloed away with many vendors. Data out looks different vendor to vendor. At best, the vendor may have an Ed-Fi integration or offer a comprehensive rest API. Some may offer the ability to extract a subset of the data to a SFTP server. Others may offer a manual export option in app. Finally, others may not offer any form of data out.

Should an analytics engineer gain access to the data, it is going to look very different vendor to vendor. Each vendor has their own way of organizing the data and their own terminology.

The task ahead for every analytics engineer is to gather all data necessary for their use cases into a common data warehouse so it may be cleaned, transformed, and prepared for use in analytics. This also involves maintaining documentation and tests around the data to ensure it is well understood and accurate.
