# Technical Assignment Week 8

    from flask import Flask

    from flask import jsonify

    from flask import request

    import os

    import pymongo

    import time

    import uuid

    app = Flask(__name__)

    client = pymongo.MongoClient(
    f"mongodb+srv://adri:{os.getenv('PW')}@cluster0.mzhjnwo.mongodb.net/?retryWrites=true&w=majority")
    db = client["sic-db"]


    @app.route("/", methods=['POST'])
    def data():
    if request.method == "POST":

        data = request.get_json()

        _id = int(str(uuid.uuid1().int)[:7])
        kecepatan = data.get("kecepatan")
        latitude = data.get("latitude")
        longitude = data.get("longitude")
        timestamp = time.time()

        json = {"transaction_id": _id, "kecepatan": kecepatan,
                "latitude": latitude, "longitude": longitude, "timestamp": timestamp}

        koneksi = db["technical-assignment"]

        koneksi.insert_one(json)

        return "Data Ditambahkan"


    if __name__ == "__main__":
    app.run(host="127.0.0.1", port=8000, debug=True)


