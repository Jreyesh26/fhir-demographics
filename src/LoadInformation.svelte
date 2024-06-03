<script lang="ts">
    import { navigate } from "svelte-routing";
    import { fhir } from "./fhir";

    // Define los datos de los pacientes predefinidos
    const pacientesPredefinidos = [
        {
            resourceType: "Patient",
            id: "1",
            name: [{ given: ["Juan Reyes"] }],
            gender: "male",
            birthDate: "1998-04-26",
        },
        {
            resourceType: "Patient",
            id: "2",
            name: [{ given: ["María López"] }],
            gender: "female",
            birthDate: "1985-09-12",
        },
        {
            resourceType: "Patient",
            id: "3",
            name: [{ given: ["Pedro García"] }],
            gender: "male",
            birthDate: "1976-07-18",
        },
        {
            resourceType: "Patient",
            id: "4",
            name: [{ given: ["Ana Martínez"] }],
            gender: "female",
            birthDate: "2000-02-03",
        },
        {
            resourceType: "Patient",
            id: "5",
            name: [{ given: ["Carlos Rodríguez"] }],
            gender: "male",
            birthDate: "1993-11-30",
        },
    ];

    const practitionersPredefinidos = [
        {
            resourceType: "Practitioner",
            id: "1",
            name: [
                {
                    family: "Gómez",
                    given: ["María"],
                },
            ],
            telecom: [
                {
                    system: "phone",
                    value: "1234567890",
                },
            ],
            gender: "female",
            birthDate: "1980-05-15",
        },
        {
            resourceType: "Practitioner",
            id: "2",
            name: [
                {
                    family: "Hernández",
                    given: ["Carlos"],
                },
            ],
            telecom: [
                {
                    system: "phone",
                    value: "0987654321",
                },
            ],
            gender: "male",
            birthDate: "1975-10-20",
        },
        {
            resourceType: "Practitioner",
            id: "3",
            name: [
                {
                    family: "Martínez",
                    given: ["Luisa"],
                },
            ],
            telecom: [
                {
                    system: "phone",
                    value: "1357924680",
                },
            ],
            gender: "female",
            birthDate: "1992-03-28",
        },
        {
            resourceType: "Practitioner",
            id: "4",
            name: [
                {
                    family: "Ramírez",
                    given: ["Javier"],
                },
            ],
            telecom: [
                {
                    system: "phone",
                    value: "9876543210",
                },
            ],
            gender: "male",
            birthDate: "1988-07-10",
        },
        {
            resourceType: "Practitioner",
            id: "5",
            name: [
                {
                    family: "López",
                    given: ["Ana"],
                },
            ],
            telecom: [
                {
                    system: "phone",
                    value: "2468013579",
                },
            ],
            gender: "female",
            birthDate: "1970-12-05",
        },
    ];

    const encountersPredefinidos = [
        {
            resourceType: "Encounter",
            id: "1",
            class: [
                {
                    coding: [
                        {
                            system: "http://terminology.hl7.org/CodeSystem/v3-ActCode",
                            code: "IMP",
                            display: "inpatient encounter",
                        },
                    ],
                },
            ],
            subject: {
                reference: "Patient/2",
            },
            participant: [
                {
                    type: [
                        {
                            coding: [
                                {
                                    system: "http://terminology.hl7.org/CodeSystem/v3-ParticipationType",
                                    code: "ATND",
                                    display: "attender",
                                },
                            ],
                        },
                    ],
                    actor: {
                        reference: "Practitioner/1",
                    },
                },
            ],
        },
        {
            resourceType: "Encounter",
            id: "2",
            class: [
                {
                    coding: [
                        {
                            system: "http://terminology.hl7.org/CodeSystem/v3-ActCode",
                            code: "AMB",
                            display: "ambulatory",
                        },
                    ],
                },
            ],
            subject: {
                reference: "Patient/2",
            },
            participant: [
                {
                    type: [
                        {
                            coding: [
                                {
                                    system: "http://terminology.hl7.org/CodeSystem/v3-ParticipationType",
                                    code: "ATND",
                                    display: "attender",
                                },
                            ],
                        },
                    ],
                    actor: {
                        reference: "Practitioner/2",
                    },
                },
            ],
        },
        {
            resourceType: "Encounter",
            id: "3",
            class: [
                {
                    coding: [
                        {
                            system: "http://terminology.hl7.org/CodeSystem/v3-ActCode",
                            code: "AMB",
                            display: "ambulatory",
                        },
                    ],
                },
            ],
            subject: {
                reference: "Patient/3",
            },
            participant: [
                {
                    type: [
                        {
                            coding: [
                                {
                                    system: "http://terminology.hl7.org/CodeSystem/v3-ParticipationType",
                                    code: "ATND",
                                    display: "attender",
                                },
                            ],
                        },
                    ],
                    actor: {
                        reference: "Practitioner/3",
                    },
                },
            ],
        },
        {
            resourceType: "Encounter",
            id: "4",
            class: [
                {
                    coding: [
                        {
                            system: "http://terminology.hl7.org/CodeSystem/v3-ActCode",
                            code: "IMP",
                            display: "inpatient encounter",
                        },
                    ],
                },
            ],
            subject: {
                reference: "Patient/4",
            },
            participant: [
                {
                    type: [
                        {
                            coding: [
                                {
                                    system: "http://terminology.hl7.org/CodeSystem/v3-ParticipationType",
                                    code: "ATND",
                                    display: "attender",
                                },
                            ],
                        },
                    ],
                    actor: {
                        reference: "Practitioner/4",
                    },
                },
            ],
        },
        {
            resourceType: "Encounter",
            id: "5",
            class: [
                {
                    coding: [
                        {
                            system: "http://terminology.hl7.org/CodeSystem/v3-ActCode",
                            code: "IMP",
                            display: "inpatient encounter",
                        },
                    ],
                },
            ],
            subject: {
                reference: "Patient/5",
            },
            participant: [
                {
                    type: [
                        {
                            coding: [
                                {
                                    system: "http://terminology.hl7.org/CodeSystem/v3-ParticipationType",
                                    code: "ATND",
                                    display: "attender",
                                },
                            ],
                        },
                    ],
                    actor: {
                        reference: "Practitioner/5",
                    },
                },
            ],
        },
    ];

    const observationsPredefinidos = [
        {
            resourceType: "Observation",
            category: [
                {
                    coding: [
                        {
                            system: "http://terminology.hl7.org/CodeSystem/observation-category",
                            code: "vital-signs",
                            display: "Vital Signs",
                        },
                    ],
                },
            ],
            code: {
                coding: [
                    {
                        system: "http://loinc.org",
                        code: "55284-4",
                        display: "Blood pressure systolic and diastolic",
                    },
                ],
            },
            subject: {
                reference: "Patient/1",
            },
            encounter: {
                reference: "Encounter/13",
            },
            performer: [
                {
                    reference: "Practitioner/2",
                },
            ],
            effectiveDateTime: "2024-06-03T10:00:00Z",
            valueQuantity: {
                value: 120,
                unit: "mmHg",
                system: "http://unitsofmeasure.org",
                code: "mm[Hg]",
            },
        },
    ];

    // Función para enviar los pacientes predefinidos al servidor FHIR
    async function enviarPacientesPredefinidos() {
        for (const paciente of pacientesPredefinidos) {
            try {
                const response = await fhir.post("/Patient", paciente);
                console.log(
                    `Paciente ${paciente.id} enviado exitosamente al servidor FHIR:`,
                    response.data,
                );
            } catch (error) {
                console.error(
                    `Error al enviar paciente ${paciente.id} al servidor FHIR:`,
                    error,
                );
            }
        }
    }

    async function enviarpractitionersPredefinidos() {
        for (const practitioner of practitionersPredefinidos) {
            try {
                const response = await fhir.post("/Practitioner", practitioner);
                console.log(
                    `Practitioner ${practitioner.name[0].given} enviado exitosamente al servidor FHIR:`,
                    response.data,
                );
            } catch (error) {
                console.error(
                    `Error al enviar paciente ${practitioner.name[0].given}} al servidor FHIR:`,
                    error,
                );
            }
        }
    }

    async function enviarencountersPredefinidos() {
        for (const encounter of encountersPredefinidos) {
            try {
                const response = await fhir.post("/Encounter", encounter);
                console.log(response.data);
            } catch (error) {
                console.error(error);
            }
        }
    }

    async function enviarobservationsPredefinidos() {
        for (const observation of observationsPredefinidos) {
            try {
                const response = await fhir.post("/Observation", observation);
                console.log(response.data);
            } catch (error) {
                console.error(error);
            }
        }
    }
    // Llamamos a la función para enviar los pacientes predefinidos
    enviarPacientesPredefinidos();
    enviarpractitionersPredefinidos();
    enviarencountersPredefinidos();
    enviarobservationsPredefinidos();
    navigate("/", { replace: true });
</script>
