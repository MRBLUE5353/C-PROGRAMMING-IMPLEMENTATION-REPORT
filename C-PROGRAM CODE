#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_RECORDS 100
#define FILE_NAME "service_records.dat"

typedef struct
{
    char vehicleNumber[20];
    char customerName[50];
    char vehicleModel[50];
    char serviceType[50];
    char serviceDate[15];
    float partsCost;
    float labourCost;
    float totalServiceCost;
} ServiceRecord;


/* Function Prototypes */
void calculateTotal(ServiceRecord *record);
void updateServiceRecord(ServiceRecord *record);
void registerVehicle(ServiceRecord records[], int *count);
void searchVehicle(ServiceRecord records[], int count);
void updateVehicle(ServiceRecord records[], int count);
void calculateBill(ServiceRecord records[], int count);
void sortByServiceCost(ServiceRecord records[], int count);
void displayAboveAmount(ServiceRecord records[], int count);
void dailySummary(ServiceRecord records[], int count);
void displayAll(ServiceRecord records[], int count);
void saveRecords(ServiceRecord records[], int count);
void loadRecords(ServiceRecord records[], int *count);
void displayRecord(ServiceRecord *record);
int findVehicle(ServiceRecord records[], int count, char vehicleNumber[]);
int isValidDate(char date[]);
float readValidCost(char message[]);


/* Calculate total cost using pointer */
void calculateTotal(ServiceRecord *record)
{
    record->totalServiceCost =
        record->partsCost + record->labourCost;
}


/* Validate date */
int isValidDate(char date[])
{
    int day, month, year;

    if (strlen(date) != 10)
        return 0;

    if (date[2] != '-' || date[5] != '-')
        return 0;

    if (sscanf(date, "%2d-%2d-%4d",
               &day, &month, &year) != 3)
        return 0;

    if (day < 1 || day > 31)
        return 0;

    if (month < 1 || month > 12)
        return 0;

    if (year < 2000 || year > 2100)
        return 0;

    return 1;
}


/* Read valid cost */
float readValidCost(char message[])
{
    float cost;

    while (1)
    {
        printf("%s", message);

        if (scanf("%f", &cost) != 1)
        {
            printf("Invalid input! Enter a numeric value.\n");

            while (getchar() != '\n');

            continue;
        }

        if (cost < 0)
        {
            printf("Cost cannot be negative.\n");
            continue;
        }

        getchar();
        return cost;
    }
}


/* Find vehicle */
int findVehicle(ServiceRecord records[],
                int count,
                char vehicleNumber[])
{
    int i;

    for (i = 0; i < count; i++)
    {
        if (strcmp(records[i].vehicleNumber,
                   vehicleNumber) == 0)
        {
            return i;
        }
    }

    return -1;
}


/* Register vehicle */
void registerVehicle(ServiceRecord records[], int *count)
{
    ServiceRecord *record;

    if (*count >= MAX_RECORDS)
    {
        printf("\nMaximum record capacity reached!\n");
        return;
    }

    record = &records[*count];

    printf("\n========== REGISTER VEHICLE ==========\n");

    printf("Enter Vehicle Number: ");
    scanf("%19s", record->vehicleNumber);
    getchar();

    if (findVehicle(records,
                    *count,
                    record->vehicleNumber) != -1)
    {
        printf("Duplicate vehicle number!\n");
        return;
    }

    printf("Enter Customer Name: ");
    fgets(record->customerName,
          sizeof(record->customerName), stdin);

    record->customerName[
        strcspn(record->customerName, "\n")
    ] = '\0';


    printf("Enter Vehicle Model: ");
    fgets(record->vehicleModel,
          sizeof(record->vehicleModel), stdin);

    record->vehicleModel[
        strcspn(record->vehicleModel, "\n")
    ] = '\0';


    printf("Enter Service Type: ");
    fgets(record->serviceType,
          sizeof(record->serviceType), stdin);

    record->serviceType[
        strcspn(record->serviceType, "\n")
    ] = '\0';


    do
    {
        printf("Enter Service Date (DD-MM-YYYY): ");
        scanf("%14s", record->serviceDate);
        getchar();

        if (!isValidDate(record->serviceDate))
            printf("Invalid date! Try again.\n");

    } while (!isValidDate(record->serviceDate));


    record->partsCost =
        readValidCost("Enter Parts Cost: ");

    record->labourCost =
        readValidCost("Enter Labour Cost: ");

    calculateTotal(record);

    (*count)++;

    printf("\nVehicle registered successfully!\n");
    printf("Total Service Cost: Rs. %.2f\n",
           record->totalServiceCost);
}


/* Display record */
void displayRecord(ServiceRecord *record)
{
    printf("\n--------------------------------------\n");
    printf("Vehicle Number : %s\n", record->vehicleNumber);
    printf("Customer Name  : %s\n", record->customerName);
    printf("Vehicle Model  : %s\n", record->vehicleModel);
    printf("Service Type   : %s\n", record->serviceType);
    printf("Service Date   : %s\n", record->serviceDate);
    printf("Parts Cost     : Rs. %.2f\n", record->partsCost);
    printf("Labour Cost    : Rs. %.2f\n", record->labourCost);
    printf("Total Cost     : Rs. %.2f\n",
           record->totalServiceCost);
    printf("--------------------------------------\n");
}


/* Search vehicle */
void searchVehicle(ServiceRecord records[], int count)
{
    char number[20];
    int index;

    printf("\nEnter Vehicle Number: ");
    scanf("%19s", number);
    getchar();

    index = findVehicle(records, count, number);

    if (index == -1)
    {
        printf("Vehicle not found!\n");
    }
    else
    {
        displayRecord(&records[index]);
    }
}


/* Update service record */
void updateServiceRecord(ServiceRecord *record)
{
    int choice;

    printf("\n========== UPDATE SERVICE ==========\n");
    printf("1. Customer Name\n");
    printf("2. Vehicle Model\n");
    printf("3. Service Type\n");
    printf("4. Service Date\n");
    printf("5. Parts Cost\n");
    printf("6. Labour Cost\n");

    printf("Enter choice: ");
    scanf("%d", &choice);
    getchar();

    switch (choice)
    {
        case 1:
            printf("Enter Customer Name: ");
            fgets(record->customerName,
                  sizeof(record->customerName), stdin);

            record->customerName[
                strcspn(record->customerName, "\n")
            ] = '\0';
            break;

        case 2:
            printf("Enter Vehicle Model: ");
            fgets(record->vehicleModel,
                  sizeof(record->vehicleModel), stdin);

            record->vehicleModel[
                strcspn(record->vehicleModel, "\n")
            ] = '\0';
            break;

        case 3:
            printf("Enter Service Type: ");
            fgets(record->serviceType,
                  sizeof(record->serviceType), stdin);

            record->serviceType[
                strcspn(record->serviceType, "\n")
            ] = '\0';
            break;

        case 4:
        {
            char date[15];

            printf("Enter Service Date (DD-MM-YYYY): ");
            scanf("%14s", date);
            getchar();

            if (isValidDate(date))
                strcpy(record->serviceDate, date);
            else
                printf("Invalid date!\n");

            break;
        }

        case 5:
            record->partsCost =
                readValidCost("Enter Parts Cost: ");
            break;

        case 6:
            record->labourCost =
                readValidCost("Enter Labour Cost: ");
            break;

        default:
            printf("Invalid choice!\n");
            return;
    }

    calculateTotal(record);

    printf("Service details updated successfully!\n");
}


/* Update vehicle */
void updateVehicle(ServiceRecord records[], int count)
{
    char number[20];
    int index;

    printf("\nEnter Vehicle Number: ");
    scanf("%19s", number);
    getchar();

    index = findVehicle(records, count, number);

    if (index == -1)
    {
        printf("Vehicle not found!\n");
        return;
    }

    updateServiceRecord(&records[index]);
}


/* Calculate bill */
void calculateBill(ServiceRecord records[], int count)
{
    char number[20];
    int index;

    printf("\nEnter Vehicle Number: ");
    scanf("%19s", number);
    getchar();

    index = findVehicle(records, count, number);

    if (index == -1)
    {
        printf("Vehicle not found!\n");
        return;
    }

    calculateTotal(&records[index]);

    printf("\n========== SERVICE BILL ==========\n");
    printf("Vehicle Number : %s\n",
           records[index].vehicleNumber);

    printf("Customer       : %s\n",
           records[index].customerName);

    printf("Vehicle Model  : %s\n",
           records[index].vehicleModel);

    printf("Service Type   : %s\n",
           records[index].serviceType);

    printf("Parts Cost     : Rs. %.2f\n",
           records[index].partsCost);

    printf("Labour Cost    : Rs. %.2f\n",
           records[index].labourCost);

    printf("----------------------------------\n");

    printf("TOTAL BILL     : Rs. %.2f\n",
           records[index].totalServiceCost);

    printf("==================================\n");
}


/* Bubble Sort */
void sortByServiceCost(ServiceRecord records[], int count)
{
    int i, j;
    ServiceRecord temp;

    if (count < 2)
    {
        printf("Not enough records to sort.\n");
        return;
    }

    for (i = 0; i < count - 1; i++)
    {
        for (j = 0; j < count - i - 1; j++)
        {
            if (records[j].totalServiceCost >
                records[j + 1].totalServiceCost)
            {
                temp = records[j];
                records[j] = records[j + 1];
                records[j + 1] = temp;
            }
        }
    }

    printf("\nRecords sorted by service cost successfully!\n");
}


/* Display above specified amount */
void displayAboveAmount(ServiceRecord records[], int count)
{
    float amount;
    int i;
    int found = 0;

    amount =
        readValidCost("\nEnter Amount: ");

    printf("\nVehicles with service cost above Rs. %.2f\n",
           amount);

    for (i = 0; i < count; i++)
    {
        if (records[i].totalServiceCost > amount)
        {
            displayRecord(&records[i]);
            found = 1;
        }
    }

    if (!found)
        printf("No vehicles found above this amount.\n");
}


/* Daily summary */
void dailySummary(ServiceRecord records[], int count)
{
    char date[15];
    int i;
    int totalVehicles = 0;
    float totalRevenue = 0;

    printf("\nEnter Date (DD-MM-YYYY): ");
    scanf("%14s", date);
    getchar();

    if (!isValidDate(date))
    {
        printf("Invalid date!\n");
        return;
    }

    printf("\n========== DAILY SERVICE SUMMARY ==========\n");
    printf("Date: %s\n", date);

    for (i = 0; i < count; i++)
    {
        if (strcmp(records[i].serviceDate, date) == 0)
        {
            totalVehicles++;

            totalRevenue +=
                records[i].totalServiceCost;

            printf("%d. %s - Rs. %.2f\n",
                   totalVehicles,
                   records[i].vehicleNumber,
                   records[i].totalServiceCost);
        }
    }

    printf("-------------------------------------------\n");
    printf("Total Vehicles : %d\n", totalVehicles);
    printf("Total Revenue  : Rs. %.2f\n", totalRevenue);
    printf("===========================================\n");
}


/* Display all records */
void displayAll(ServiceRecord records[], int count)
{
    int i;

    if (count == 0)
    {
        printf("\nNo records available.\n");
        return;
    }

    printf("\n========== ALL SERVICE RECORDS ==========\n");

    for (i = 0; i < count; i++)
    {
        displayRecord(&records[i]);
    }
}


/* Save records */
void saveRecords(ServiceRecord records[], int count)
{
    FILE *file;

    file = fopen(FILE_NAME, "wb");

    if (file == NULL)
    {
        printf("ERROR: Unable to open file for saving.\n");
        return;
    }

    if (fwrite(&count,
               sizeof(int),
               1,
               file) != 1)
    {
        printf("ERROR: Unable to save record count.\n");
        fclose(file);
        return;
    }

    if (count > 0)
    {
        if (fwrite(records,
                   sizeof(ServiceRecord),
                   count,
                   file) != (size_t)count)
        {
            printf("ERROR: Unable to save records.\n");
            fclose(file);
            return;
        }
    }

    fclose(file);

    printf("Records saved successfully!\n");
}


/* Load records */
void loadRecords(ServiceRecord records[], int *count)
{
    FILE *file;
    int storedCount;

    file = fopen(FILE_NAME, "rb");

    if (file == NULL)
    {
        printf("No previous records found.\n");
        printf("Starting new database.\n");
        *count = 0;
        return;
    }

    if (fread(&storedCount,
              sizeof(int),
              1,
              file) != 1)
    {
        printf("ERROR: Invalid file data.\n");
        fclose(file);
        *count = 0;
        return;
    }

    if (storedCount < 0 ||
        storedCount > MAX_RECORDS)
    {
        printf("ERROR: Invalid record count.\n");
        fclose(file);
        *count = 0;
        return;
    }

    if (storedCount > 0)
    {
        if (fread(records,
                  sizeof(ServiceRecord),
                  storedCount,
                  file) != (size_t)storedCount)
        {
            printf("ERROR: Incomplete file data.\n");
            fclose(file);
            *count = 0;
            return;
        }
    }

    *count = storedCount;

    fclose(file);

    printf("%d previous records loaded successfully.\n",
           *count);
}


/* Main function */
int main()
{
    ServiceRecord records[MAX_RECORDS];

    int count = 0;
    int choice;

    loadRecords(records, &count);

    do
    {
        printf("\n\n");
        printf("=============================================\n");
        printf("    AUTOMOBILE SERVICE CENTRE MANAGEMENT\n");
        printf("=============================================\n");
        printf("1. Register Vehicle\n");
        printf("2. Search Vehicle\n");
        printf("3. Update Service Details\n");
        printf("4. Calculate Total Bill\n");
        printf("5. Sort Vehicles by Service Cost\n");
        printf("6. Display Vehicles Above Amount\n");
        printf("7. Generate Daily Service Summary\n");
        printf("8. Display All Records\n");
        printf("9. Save Records\n");
        printf("0. Exit\n");
        printf("=============================================\n");

        printf("Enter your choice: ");

        if (scanf("%d", &choice) != 1)
        {
            printf("Invalid menu input!\n");

            while (getchar() != '\n');

            continue;
        }

        getchar();

        switch (choice)
        {
            case 1:
                registerVehicle(records, &count);
                break;

            case 2:
                searchVehicle(records, count);
                break;

            case 3:
                updateVehicle(records, count);
                break;

            case 4:
                calculateBill(records, count);
                break;

            case 5:
                sortByServiceCost(records, count);
                break;

            case 6:
                displayAboveAmount(records, count);
                break;

            case 7:
                dailySummary(records, count);
                break;

            case 8:
                displayAll(records, count);
                break;

            case 9:
                saveRecords(records, count);
                break;

            case 0:
                saveRecords(records, count);
                printf("\nThank you for using the system!\n");
                break;

            default:
                printf("Invalid choice! Try again.\n");
        }

    } while (choice != 0);

    return 0;
}
