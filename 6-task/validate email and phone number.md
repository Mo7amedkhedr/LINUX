

# Validating Email Addresses


grep -E '^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$' filename.txt


# Validating Phone Numbers

grep -E '^\(?[0-9]{3}\)?[-. ]?[0-9]{3}[-. ]?[0-9]{4}$' filename.txt
